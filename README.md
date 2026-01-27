# Runbook — Simulador de Adquirência (Merchant → Settlement)

Data: 2026-01-27

## Architecture
<img width="907" height="722" alt="image" src="https://github.com/user-attachments/assets/2a8d4a4c-b601-49a4-bc81-6b4377213a78" />


Este documento complementa os READMEs individuais e mostra:

1. Como subir **infra** e **cada serviço** (um por vez) usando Docker.
2. Um **End-to-End passo a passo** do fluxo: `merchant-api` → `acquirer-core` → (`risk-engine`, `issuer-simulator`) → `clearing-service` → `settlement-service` → volta no `acquirer-core` com `settlement.completed`.

> Premissas
- Você usa um `docker-compose.infra.yml` compartilhado (Kafka + Redis + Postgres).
- Cada serviço tem seu próprio `docker-compose.yml` (apenas o app), apontando para a infra via network `acquiring-net`.
- Postgres é **único** e possui múltiplos databases (ex.: `acquiring`, `clearing`, `settlement`), criados via `postgres-init/01-create-dbs.sql`.

---

## 0) Pré-requisitos

- Docker + Docker Compose v2
- Java 21 + Maven (para rodar local, opcional)

Rede Docker (crie uma vez):
```bash
docker network create acquiring-net || true
```

---

## 1) Subir Infra (Kafka + Redis + Postgres)

### 1.1 Estrutura esperada
Na pasta da infra:
```
docker-compose.infra.yml
postgres-init/01-create-dbs.sql
```

Exemplo de `postgres-init/01-create-dbs.sql`:
```sql
SELECT 'CREATE DATABASE acquiring'
WHERE NOT EXISTS (SELECT FROM pg_database WHERE datname = 'acquiring')\gexec;

SELECT 'CREATE DATABASE clearing'
WHERE NOT EXISTS (SELECT FROM pg_database WHERE datname = 'clearing')\gexec;

SELECT 'CREATE DATABASE settlement'
WHERE NOT EXISTS (SELECT FROM pg_database WHERE datname = 'settlement')\gexec;
```

### 1.2 Subir
```bash
docker compose -f docker-compose.infra.yml up -d
```

> Se você adicionou novos DBs no init, rode com reset (dev):
```bash
docker compose -f docker-compose.infra.yml down -v
docker compose -f docker-compose.infra.yml up -d
```

### 1.3 Verificar
- Kafka: `localhost:9092` (do host)
- Redis: `localhost:6379`
- Postgres: `localhost:5432`

Listar databases:
```bash
PG=$(docker ps --format "{{.Names}} {{.Image}}" | awk '$2 ~ /^postgres/ {print $1; exit}')
docker exec -it "$PG" psql -U postgres -c "\l"
```

---

## 2) Subir serviços (um por vez)

A ordem recomendada (para E2E):
1) `card-certifier`
2) `brand-network-hub`
3) `acquirer-core`
4) `risk-engine`
5) `issuer-simulator`
6) `clearing-service`
7) `settlement-service`
8) `merchant-api`

> Regra: os serviços **não** sobem Postgres/Kafka/Redis próprios. Eles usam o infra via `acquiring-net`.

### 2.1 card-certifier
```bash
cd card-certifier
docker compose up -d --build
curl -s http://localhost:8086/actuator/health
```

### 2.2 brand-network-hub
```bash
cd ../brand-network-hub
docker compose up -d --build
curl -s http://localhost:8087/actuator/health
```

### 2.3 acquirer-core
```bash
cd ../acquirer-core
docker compose up -d --build
curl -s http://localhost:8081/actuator/health
```

### 2.4 risk-engine
```bash
cd ../risk-engine
docker compose up -d --build
curl -s http://localhost:8083/actuator/health
```

### 2.5 issuer-simulator
```bash
cd ../issuer-simulator
docker compose up -d --build
curl -s http://localhost:8084/actuator/health
```

### 2.6 clearing-service
```bash
cd ../clearing-service
docker compose up -d --build
curl -s http://localhost:8088/actuator/health
```

### 2.7 settlement-service
```bash
cd ../settlement-service
docker compose up -d --build
curl -s http://localhost:8091/actuator/health
```

### 2.8 merchant-api
```bash
cd ../merchant-api
docker compose up -d --build
curl -s http://localhost:8080/actuator/health
```

---

## 3) End-to-End (Merchant → Settlement) — passo a passo

### 3.1 Visão geral
O fluxo tem duas “pernas”:

- **Síncrona (HTTP)**: merchant → merchant-api → acquirer-core (authorize/capture/get)
- **Assíncrona (Kafka)**: acquirer-core ↔ risk-engine ↔ issuer-simulator ↔ clearing-service ↔ settlement-service → volta ao acquirer-core

### 3.2 Passo a passo detalhado (quem chama quem)

#### Passo 1 — Merchant autoriza pagamento
1) Merchant chama `merchant-api`:
- `POST /v1/payments/authorize`
- Header: `Idempotency-Key`

2) `merchant-api` valida payload e **encaminha** para `acquirer-core`:
- `POST /payments/authorize`
- repassa `Idempotency-Key` e `X-Correlation-Id` (se houver)

3) `acquirer-core` aplica **idempotência** (Redis):
- Se a chave já existe → retorna o mesmo `paymentId` (não duplica eventos)
- Se não existe → cria `Payment` (DB `acquiring`), grava `OutboxEvent` e responde **200** com `paymentId` + status inicial.

4) `acquirer-core` (via Outbox) publica evento Kafka:
- `payment.authorize.requested`

#### Passo 2 — Risk Engine decide risco
5) `risk-engine` consome `payment.authorize.requested`
6) Aplica regras (ex.: limite, bloqueio por last4) e publica (via outbox):
- `payment.risk.approved` **ou**
- `payment.risk.rejected`

#### Passo 3 — Issuer autoriza/declina
7) `issuer-simulator` consome:
- `payment.risk.approved` → avalia issuer rules e publica:
  - `payment.authorized` ou `payment.declined`
- `payment.risk.rejected` → publica diretamente:
  - `payment.declined` (reason = `risk_rejected`)

#### Passo 4 — acquirer-core atualiza status
8) `acquirer-core` consome `payment.authorized` / `payment.declined`:
- Atualiza `Payment.status` para `AUTHORIZED` ou `DECLINED`

9) Merchant consulta status:
- `GET /v1/payments/{paymentId}` → merchant-api → acquirer-core

#### Passo 5 — Merchant captura (se autorizado)
10) Merchant chama:
- `POST /v1/payments/{paymentId}/capture`

11) merchant-api encaminha para:
- `POST /payments/{paymentId}/capture` no `acquirer-core`

12) `acquirer-core` valida:
- Só captura se status == `AUTHORIZED`
- Grava `OutboxEvent` e publica:
  - `payment.capture.requested`

#### Passo 6 — Clearing agrega e emite "captured"
13) `clearing-service` consome `payment.capture.requested`
14) Cria/atualiza **batch** (DB `clearing`):
- tabela `clearing_batch` e `clearing_batch_item`
15) Ao fechar o batch (por tamanho/tempo), publica:
- `payment.captured` (um por payment) **ou** um evento agregado (depende do seu contrato)

#### Passo 7 — Settlement finaliza e emite settlement.completed
16) `settlement-service` consome `payment.captured`
17) Agrupa em batch (DB `settlement`) e, ao fechar, publica:
- `settlement.completed` com lista `paymentIds: [ ... ]`

#### Passo 8 — acquirer-core marca SETTLED
18) `acquirer-core` consome `settlement.completed`
19) Marca cada payment como `SETTLED`
20) Merchant consulta:
- `GET /v1/payments/{paymentId}` → status `SETTLED`

---

## 4) Comandos de teste E2E (curl)

### 4.1 Autorizar
```bash
curl -i -X POST http://localhost:8080/v1/payments/authorize \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: idem-001" \
  -H "X-Correlation-Id: corr-001" \
  -d '{
    "merchantId":"m1",
    "orderId":"o1",
    "amountCents":1000,
    "currency":"BRL",
    "card":{"pan":"4111111111111111","holderName":"JOAO","expMonth":"12","expYear":"2030","cvv":"123"}
  }'
```

Pegue o `paymentId` do JSON retornado.

### 4.2 Consultar
```bash
curl -s http://localhost:8080/v1/payments/<paymentId> | jq .
```

### 4.3 Capturar
```bash
curl -i -X POST http://localhost:8080/v1/payments/<paymentId>/capture
```

### 4.4 Acompanhar até SETTLED
```bash
watch -n 1 "curl -s http://localhost:8080/v1/payments/<paymentId> | jq -r '.status'"
```

---

## 5) Observabilidade rápida

- Health (todos): `GET /actuator/health`
- Prometheus (todos): `GET /actuator/prometheus`

Exemplos:
```bash
curl -s http://localhost:8081/actuator/health
curl -s http://localhost:8091/actuator/prometheus | head
```

Logs estruturados (JSON) saem no stdout do container:
```bash
docker logs -f settlement-service
```

---

## 6) Troubleshooting (mais comuns)

### “database X does not exist”
- Você não criou o DB no init (ou o volume já existia).
- Solução dev:
```bash
docker compose -f docker-compose.infra.yml down -v
docker compose -f docker-compose.infra.yml up -d
```

### Flyway não criou tabelas
- Migration fora do path: `src/main/resources/db/migration`
- Nome incorreto: `V1__init.sql`
- Verifique `flyway_schema_history` no DB.

### Kafka dentro do Docker
- Quando o app roda em container, preferir `kafka:29092` (listener interno).
- Quando o app roda no host, usar `localhost:9092`.

---

## 7) Mapa rápido de portas (padrão)
- merchant-api: 8080
- acquirer-core: 8081
- risk-engine: 8083
- issuer-simulator: 8084
- card-certifier: 8086
- brand-network-hub: 8087
- clearing-service: 8088
- settlement-service: 8091
