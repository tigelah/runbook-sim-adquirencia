# Runbook — Simulador de Adquirência (Merchant → Settlement)

Data: 2026-01-27

## Architecture
[<img width="907" height="722" alt="image" src="https://github.com/user-attachments/assets/2a8d4a4c-b601-49a4-bc81-6b4377213a78" />](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=HLD-prod-k8s-gitops.drawio&dark=auto#R%3Cmxfile%20pages%3D%221%22%3E%3Cdiagram%20name%3D%22High%20Level%20Design%20(Prod)%22%20id%3D%220%22%3E7V3tk6I4Gv9b9oNVM1elRcL7R%2FttZ%2Btmbvum5253P3VFiMo2ggfYds9ffwkkCgEVENBWumZKCSHEPG%2B%2F50nyZCDfLt5%2BDdBy%2Fs23sTuAkv02kO8GEAJNM8kHLXlPSkygJAWzwLFZpW3Bk%2FMTs0KJla4cG4eZipHvu5GzzBZavudhK8qUoSDw19lqU9%2FNvnWJZjhX8GQhN1%2F6h2NHc1ZqSNL2xhfszOb81RK%2Fs0C8NisI58j216ki%2BX4g3wa%2BHyXfFm%2B32KWjxwcmee5hx91NzwLsRWUemPwA7vrnF%2Fn31U%2F44qzMuX%2FzbajmW2ENh9E7H4Sl73hRPJDqDflHXnMrDVRy55ZejaAqFIjXerYA5K9oG9kC8VrPFgCxeSC8H4gdTBXkrjLNS8L7pVQHyT%2F5xl9FruPh2w3LSaRwFiDbIWN467t%2BQMo83yOjdzOPFi65AuTreu5E%2BGmJLDqqayIupGzqexFjegD5NRt42iph6wiRdwWsjZgSOLh%2FxQlBkjqui5ahM9k8FWBrFYTOK%2F6Ow6RxWkr4b0m%2FL95mVFZHaB0qo1ngr5Zx938j7yq8%2B%2Fy6tGjfwijwXzD%2FfQMoG7fKw8MD7bXjusLvfsVB5BAxGrvOjDYb%2BfQtiF25eBrRFslgON7sa3x1J0tsAFKvGI9v9BuDlNsonGOb%2FZKEQV%2BRu2IM%2Bt%2FHW1ZGXovfUnzMROFX7C9wFLyTKvOUtGo6TJ5bb2XbUJm8vgnXTINpGrtGTLXMNm1vhY98YfJXQRa1vCzuk9leQHsBTQQ0pM050fvztvJTLKy8YVFy9fEYAE2QXFL%2BAB%2B0e6M58YWKYRCDf0h8H1cT17EoS68mHo5qiTLkYlkkykx0IWxJcgHUS8qulpPdAuWZo5c61m4NLT2OYCeRRA4VSLJpqojbU8KQI1ItqgCQp4opZ%2FQr1LNEkvW2iCTVplH4giNrzga0UNkWKtwipVuoePPKN1MtVocFbxALi8r0fCHIV%2BMaNF9YVFZkLsSnQcHTQHh6t7IW9YgMHyilRX21QSA5iZnGf6Lm4RLzFU2w%2B%2BiHTuTEOnXiR5G%2FOKj3LEx1e1ZODhkIFC6TnzV13mg%2FirV8gEN%2FFVg40fHEPoRF2p5o9wg%2Fq3Jj4qnkpVPJoh8AYEY6dTBSK8vnf0Ic%2FD75m44DlFw69rzPmhuxMcsInPa%2Flc9vDBMLOSYVgLR8i387v0%2B%2Bzdhn3NCEF%2FxjFOKV7S8cz%2FFHFiEtq0A6NhEfImVJB3gxPKhJ0kPLVE8NrUIoFR1WxDnmq2ceC%2FSwgHP1DKEBqENpcpkidgXlzBm4V84Xo5zv7mRFub0a5bxG08b0MpRz0goPoCajJdTE39u5fksPYaKoib%2FhFZoJK2EtaiKC2eQTlQPylX98jtuUYlsyRQvHfU%2BqfsHuK6YMlbrP2qa3PT9YIDd17xUFDiKfpL8oWgU0Krm3noWWBVVcHJGfOWS%2BU%2F6%2BHyznyGMPwqSMDuTQ8eyYALSc28HkThSQB6akDd5a7EQk7BMHQFNNrf3Azr5809ZwjScvDmmOtpnI7JAxYKZeTM%2B4jYKRmiDrhXqhnj0UqEJ8wYQgUDHZF5XTJn6ljS0%2FQFToh9HcsV48HLK%2BEyseOfwNYt0UyfbWS3UnU2%2Fq%2BigSR852wqWL3nl1qgPJl1%2BcxdIPIuRFe1FI83Dmj%2FHDgFpw2rXvKKJ9%2BeosnKgSrNkUJ3KURjvHgwkgSXv1E%2BDPNK%2BglB45XBhyuDK3Di2dZ2JS8JoqnM48O2hqHOB%2FLN9u%2FPgbqf8rG7BGHTuoXqBjB3U5q4ql6hG22n4dUBlLYTs30VpyXGMJKhHXSxGAvoxLKzHYc3%2Fme8i935bexBBlo0C2db76VDXE9PmbILV3pgPQKvKz1CN9D97%2FZM%2FHF3%2FRCyJB7PLuLX3z7p2rQNdfjz1ngZiOitt6c6I%2FU99TLZGrbUP04j118YgDh1AunnzYBtYjFMzwvoFl0eo8XwXYJd16zdKpiEvYo4%2FUZKZiRYY%2BMlN%2FejaiYJojFehQAbJuykDidpu3n9CZNZmexhbeAk0j8xY1q8RMIcafjEau2Zi%2FNz%2F9iKAyj2azBQhownmwbLR5IyEC%2F35NdOlejSHatYVj2wl703kltJ1wyoKbuyIz8%2BPr0wZjLgM%2FijV6SYVUyDjskaE0AoqRJVJ51uJV%2FOk0xO1QEFRVSD2A7AHkWQHI16X1vAycVwKJyJC9dBiGkoGWEezWwlBy7%2BVdmpDe3%2Bk0anAtQuqixcRGHTp4ipwNwdRy78qifL11lM%2BXWHwMmB9fifi8CPuXxOyJ%2FjsCsh9FX7WHSJemfW9NqMYMeB3a13730MK3Jx3qX7UJ%2FXsovDY5NraGFpRM3iSkH%2BMVUZABeS4ojqsdDKCpUmrkPmwATZzMUKQsJTuNoKlK26aVr5Ls2LKyoNc20PVX6k5x0KukscxwYYPG8pAw7pygrh3r%2Fu67OCS9eLL8Jf2yN9idn9fbz1jyJcqqekpZhVLZNfz9OmAIdEHLwizlWlsIXD4228PZjwJnr2yxmUV7NyX9i%2FDzAnlohoPn5pYFl1h%2BZmbnFFuL%2B4HSgb9%2BV1T2%2Ff2uqKq7oiRprIwLdkXdaw%2Fag35QJ5TeFQUU%2Ff5mLGqknOg%2BJhH9wVHbomQzb3hz26IM2JL0yrCk8G7EvCIgMvU7Sdc%2FICCS1QK6wCwggiKZPoDDgqz%2FrZwAB0PLD3Cz%2FgqQ08sWyjosRZx1XutzgKyOeCe508K5o5MlOhqDudUjDNvBPRi%2Bl80cGToIMhwRcQfQLKZutVUy4yCgq9Q2FRgo2bYsLG%2BRBeUMTC1N9IP142XWe%2Bqryt765EvS42bXWHDq1xLX3uc6T5%2FryiZwp0RjUDzW2AwCzFkGXsQBgGFkdYHe%2FARC8xAgcMKXIfZm8Z6JRgGAUmd24fwBANRE6y93aP110IH1V0Bv%2FctY%2F5x1Nitac7MLa65U55DemvfW%2FMqtuQpMwZpXd%2FK6t%2BaWi1HgeLMhefOrYzVu0uFFmvTcLGSnDr1ee8lAFZMu9ya9jEnXNLDP4T4TB10pu82%2FN%2Bm9Se9NOpdtQVaBXt1z696kh0TDuniB6ePtGPX0YuXLMeqasNmlW6OulF1a1GvoXkP3GnqzdFdIa8ax8VlraCcMVzRJkLNYEWhKWKJh%2FXyZE6myISQ66FY%2FNzbFVUmh7FjAU263B6t8dipGXC8Edqkd4rmFtDPWHD9P%2FeA5wLYTNqZeZC2vXqQRP9KAtSMkOorTHFRmu7KOvdSBYw8%2F3Ex9Ao1OHqs%2F4Ngr0NhXvyXHnme471mmYArj5CxjVIwFGZ2wTO2UPZfNMvJZsMwBLXMg3NgSy8DGwE%2FvnJ6Nc3plWVSSfRT2M%2Fm1GC0cbxYjyhc0fekya4M4SyjzLWXNo0mtulqv6voVjFpNnznJ58p4hd5JeZPJPfr24cK3MU%2FmyrqT97fHC%2FTTp6%2F%2FfkdzXn0ivBrNAvz076%2Bfm0yTquRoLex4k6VsWixZqe6wlqU1C4PUT1NWwAMdpCmLwy03m6TCguO6k73KZp00d0RkiL4MVwtMxnoZ%2BPYqEyHP55QswRfcBzBEa95iUhbN6ADHKfk9kp2mZdlmYvlrkE7E0k1alhPNKR9wJfMgUjb31W8JFPJAyQX6ERv%2BA4OTpgViC%2BvP3SmpuknhwCaItvze67SR%2FMxVbgNB3hyyQGwzNlAWmUffg3CL%2BWMIMy0MhTmdFpOF6sbpMLPtvBZimj3IeNdM0074XRFJN5bl%2B%2FcJXYqAJo7r2Mimm16TTLTfCMGIWOzmvR1wfVMcD9oRIN7g%2BGw3jC%2FYwCfLbc4CHBNs6XlwF%2Bb%2FzcaLpR9hz3o%2FZ24zpZGU%2FhPWpNSY3y7JdjyH85WYx6Nn9TdRhm9P%2Fzw2rLADx8v6nj3h5UwnD2R1YDtl9QhG6YPEmbKzCRJf2Qom%2FNLc8oLDwWBD2EZQIwVEyZRYoF%2F%2FfXmyeWUTOGwx0LPrI%2Ft5glzkJafcdSauQNWFI5XaO5YRHLMc%2BHycgKMdx%2FuY6Ld0BRip9uk7XQD2%2BTB%2BPxaoy9oIHoTqaoFfKI1A9T0CZbOw90r8PJV4P5xnYxPvdaKlb67GJlquv7LXiEj2MzytJeRQtoV0rseovfMxhTsDDsVn6san%2FvKffBPHZTb3XEqroY2Cl0%2BFByLHn%2FGhvPTwseQs3u2Xz%2BkTk3cuxSgfoHvCVoDp9IH0LUlV2n4c7eDSC3GDttlW2AxKtWdBmQCd7dEoNRK4F55%2B2ORc%2FqDcvCnzd4%2BdN80fTqhlw2u5FT0tH0cIAXt%2F7SDthl9PfBzhcpP9ND7SrKwS2HcSoTSSNJ665gwPIoR5CuWzJvU5ja86p3GAZ7HiLJm8mP3y1vIWF0Kj70kf65htXcojy0224jfhmomwJrcFLMvCSrgLVB7guMK9eAXkq6BnMzZ9J2jdZgJYoSFlKeQX7zCtExjJU1CAXkZb9CqLq%2FL06rXqVWtV8vU5dpSLFGthIKFZxbp5xf6E8OM%2F6Gr127ijtbRrgWwaqjEy1Yx8Drclm0nitsLYZQ93yAOhj6RiYyZvU8NqQvSltVgLkEtPO%2BQo1geYRYV8JhHR65rB7z4HCdDUkaKmlmxltasK2tsBcqx6rZnZo8JqqlTUsjBUuY1ETtHCcd%2BTql%2Bw%2B4opk6UjlUnbSTAyWCA3de8VBQ4in6S%2FKFoRzjhQzyJ4I1%2FFxVFE07IkBj1%2F3w%2BWc%2BSxB2EqVuoQk0EJQMuzUdQ4ijslbfDW2KI0yk7%2BOtvU2g%2Fs7Ms3bQ3XePLikOZom4kcDxlDZurF9IzbKBip4jhzHCam6%2FXj6DDNcpKEiTlt4lfa2PKDOKg3jOaO9eLhkPXd8Yh%2B4G8Q66ZItrdeqjuZelPXR5E4crYTLl30zqu7cR5y6RdnsfSDCLFoeWvz0TkAcPcvitqS1czfiZ7GdJZ2bzqfUktOa2iqwjP4sud6xWgwpamUrKoCUG7xDPHSu4N6aPFBoMW1HTKNIjRBYYPY4uBEqywLEpsVWK3NfQhG%2FTTDg5IzW%2FJpdpeymS3%2BPbW3r9rMFqlQc4KKacOuN%2FZBSd%2FHTqosp9km%2F7iylxuPfFxT9%2BxazTcm7%2F8pSqLp0sOX8GN7k3OV5aO3cOdu4a7s3NkwWcrBz5zt0NCpMBeWlM3mT0RsHv977iT2QwjdiA2qBP3hQY2ShA6yOqhzb7%2FxAxEVeZ%2FmVrgf08mJ7nyV75WAHLgf5RQhmu36ncFJcyFUWxPSHGTi23E5sID7D2wU6yugi1wcahmsnlcMJ0rJ1yhLlUXcUhPckyO3AaSRoSvkn6popq7CDPF1PRdQ2QFCcw2bijkyU3%2FZjDC6AUYq0Al3ybopAwlmX9LyMjRgsvfV3yus5pfqnmIZ2pcfPx6fStu5favPhnTftpFdfjYsz04drD8rSCuQ1wgXfSo3gR45cKIaAjqBQg4vWauOR7qHoQscWHM6tYGWTrMgFBgH0smfO94kqnmkZlPHE51ZI25WP3m8UZBW5sOteSibMUEuzbRjwrPkB1p0yo48mCyAGbMj5snXp9oHJDSw5gJmucjUhABTDbVQNgFMmQPbz9z92BUvrbqj4JgY62mS9xEwJhzrzHXULqgHZMPc%2B8SBUCiQZGVE%2FisG1FVDg1kQAoBRFoQ2hg8NeOEcPCg%2Fc3AMByuNcHDetxD5DShwFLOOpBlE0YkHVLcdOOcRn0bYZZPr4sJSlnatPeVGTt0oUFaGkNJKglrH7MY6XX8TFWfYE3uvAV1vMqDdfngFpYHPAS9W1s0sgWBlEmceF%2FdvtOjhglIubtuHMcXV73Yh9bObLip%2FGNNbMsfxHNovjbnkasHMEIErwhlMmjHSBQ%2BuxuFfZcGLfOHgpSMDop7kQJUa8PvQEyXg96kRN%2BR7xBti2tNm3b7OmSYAVAGWS%2Fv4sDnWKXOOQGnWOfWBAdfJOmLQuivWKZP8ojzrnM0EZWfUPi73iNyk38wOQLvWoxZOJbkqyLpLx0ouuQx8P0pXpxD%2Bm29T1%2FT%2B%2Fw%3D%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E)


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
