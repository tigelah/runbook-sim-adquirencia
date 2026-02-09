
# Lifecycle de Pagamentos (PAG-01, PAG-02, PAG-03)

## PAG-01 — Autorização & Captura

CREATED
 → AUTH_REQUESTED
 → AUTHORIZED
 → CAPTURE_REQUESTED
 → CAPTURED
 → SETTLED

Regras:
- Limites só consumidos na CAPTURE
- Ledger é fonte de verdade

## PAG-02 — Parcelamento

CREATED
 → AUTH_REQUESTED
 → AUTHORIZED (com breakdown)
 → CAPTURED (principal + juros)
 → SETTLED

Regras:
- Juros calculados no issuer
- Ledger registra principal e juros separadamente

## PAG-03 — Pré-Autorização

CREATED
 → AUTH_REQUESTED
 → AUTHORIZED_HOLD
    → CAPTURED → SETTLED
    → VOIDED
    → EXPIRED

Regras:
- HOLD reserva saldo
- VOID/EXPIRE libera reserva
- Sem settlement sem captura

## Visão Produto
- Autorização ≠ Cobrança
- Captura = dinheiro real
- Settlement = repasse financeiro
