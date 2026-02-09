
# TRD — PAG-03 (Pré-Autorização)

## Fluxo Técnico

### 1. Autorização com Reserva
Merchant → Acquirer Core → Risk → Issuer → Ledger

- Ledger cria HOLD (DEBIT)
- Estado: AUTHORIZED_HOLD
- Evento: PaymentAuthorized

### 2. Expiração Automática
Scheduler / Job / Event

- Timeout configurável (ex: 7 dias)
- Estado: EXPIRED
- Evento: AuthorizationExpired

### 3. Cancelamento Manual
Merchant → POST /payments/{id}/void

- Estado: VOIDED
- Evento: AuthorizationVoided

### 4. Ledger Reage
Para `Expired` ou `Voided`:
- RELEASE_HOLD (CREDIT)
- Nenhuma captura
- Nenhum settlement

## Regras de Consistência
- Idempotência por paymentId
- Ledger nunca duplica RELEASE_HOLD
- Eventos sempre versionáveis

## Observabilidade
- Métricas de:
  - reservas ativas
  - expiradas
  - canceladas
