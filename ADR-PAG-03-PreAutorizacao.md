
# ADR — PAG-03 (Pré-Autorização)

## Contexto
No fluxo de pagamentos, diversos casos exigem a **reserva de saldo sem captura imediata**:
- hotéis
- locadoras
- marketplaces
- ajustes manuais antes da confirmação final

Um modelo apenas com AUTH + CAPTURE imediata não atende esses cenários e gera risco financeiro.

## Decisão Arquitetural
Introduzir o conceito explícito de **Pré-Autorização (Authorization Hold)**, com:
- Reserva de saldo no ledger
- Expiração automática
- Cancelamento explícito pelo merchant
- Eventos claros e idempotentes

## Decisões
- Novo estado: `AUTHORIZED_HOLD`
- Eventos dedicados:
  - `PaymentAuthorized`
  - `AuthorizationExpired`
  - `AuthorizationVoided`
- Ledger é a fonte de verdade da reserva
- Acquirer-core apenas orquestra estados e publica eventos
- Sem captura automática

## Por quê
- Separar intenção de cobrança do consumo real
- Evitar saldo "preso" indefinidamente
- Permitir regras claras de expiração e cancelamento

## Trade-offs
### Ganhos
- Segurança financeira
- Fluxo compatível com mercado real
- Clareza para produto e engenharia

### Perdas
- Mais estados
- Mais eventos
- Complexidade operacional maior

## Quando usar
- Reservas
- Confirmações posteriores
- Produtos com risco operacional

## Quando não usar
- Pagamentos simples
- Débito imediato
