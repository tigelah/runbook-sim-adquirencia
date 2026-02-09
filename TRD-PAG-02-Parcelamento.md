# TRD — PAG-02 Parcelamento

## Fluxo Técnico
1. Merchant envia installments
2. Acquirer-core publica evento enriquecido
3. Issuer valida plano e juros
4. Ledger registra:
   - HOLD principal
   - interest virtual
5. Capture gera:
   - CAPTURE_PRINCIPAL
   - CAPTURE_INTEREST

## Componentes
- InstallmentCalculator
- CalculateInstallmentsUseCase
- LedgerEntry (principal/interest)

## Testes
- Parcelamento válido
- Parcelamento inválido
- Juros por merchant