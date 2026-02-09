# ADR — PAG-02 Parcelamento

## Contexto
Após a autorização e captura, surgiu a necessidade de suportar compras parceladas com juros configuráveis por merchant/produto.
O modelo anterior não distinguia principal de juros, inviabilizando ledger correto, settlement e refunds.

## Decisão
- Introduzir cálculo explícito de parcelamento no Issuer
- Separar principal e juros desde a autorização
- Persistir breakdown no ledger
- Eventos passam a carregar:
  - installments
  - interestCents
  - totalCents

## Justificativa
Parcelamento é decisão financeira do emissor, não do adquirente.
Separar principal/juros garante:
- Ledger correto
- Fees proporcionais
- Refunds e chargebacks futuros

## Consequências
+ Contabilidade correta
+ Auditabilidade
- Mais eventos
- Mais campos nos contratos