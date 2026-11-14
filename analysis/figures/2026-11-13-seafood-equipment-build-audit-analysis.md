# Stage 3 Build Audit — Seafood Equipment FX Hedging Model
Stage 3 Build Audit — Seafood Equipment FX Hedging Model

Finding 1 — Sensitivity Table Recalculates

What I checked:
I changed S0_in from 1.1600 to 1.1700 and reviewed the Sensitivity tab.

What I found:
The settlement-rate values and hedge proceeds changed automatically when S0_in changed.

What I did:
I changed S0_in back to 1.1600 after confirming the table was formula-driven. No correction was needed.

Finding 2 — Forward Check Figure

What I checked:
I compared the workbook’s forward proceeds against the check figure in the Stage 2 specification.

What I found:
The workbook calculated forward proceeds of $5,476,910.00, which matches the expected result based on FC_AMT = EUR 4,700,000 and F0_in = 1.1653.

What I did:
No correction was needed because the workbook passed the forward check.

Finding 3 — Money-Market Check Figure

What I checked:
I compared the money-market hedge proceeds against the check figure in the Stage 2 specification.

What I found:
The workbook calculated approximately $5,482,083.44, which matches the expected result using the placeholder spot rate, USD interest rate, EUR interest rate, and ACT/360 convention.

What I did:
No correction was needed because the workbook passed the money-market check.

Audit Conclusion

The workbook passed the three checks above. The sensitivity table is formula-driven, and the forward and money-market results match the check figures specified before the build. The workbook is ready for the next stage, where placeholder market data will be replaced with live sourced values.
## Finding 1 — Sensitivity Table Recalculates

**What I checked:**  
I changed `S0_in` from 1.1600 to 1.1700 and reviewed the Sensitivity tab.

**What I found:**  
The settlement-rate values and hedge proceeds changed automatically when `S0_in` changed.

**What I did:**  
I changed `S0_in` back to 1.1600 after confirming the table was formula-driven. No correction was needed.

## Finding 2 — Forward Check Figure

**What I checked:**  
I compared the workbook’s forward proceeds against the check figure in the Stage 2 specification.

**What I found:**  
The workbook calculated forward proceeds of **$5,476,910.00**, which matches the expected result based on `FC_AMT = EUR 4,700,000` and `F0_in = 1.1653`.

**What I did:**  
No correction was needed because the workbook passed the forward check.

## Finding 3 — Money-Market Check Figure

**What I checked:**  
I compared the money-market hedge proceeds against the check figure in the Stage 2 specification.

**What I found:**  
The workbook calculated approximately **$5,482,083.44**, which matches the expected result using the placeholder spot rate, USD interest rate, EUR interest rate, and ACT/360 convention.

**What I did:**  
No correction was needed because the workbook passed the money-market check.

## Audit Conclusion

The workbook passed the three checks above. The sensitivity table is formula-driven, and the forward and money-market results match the check figures specified before the build. The workbook is ready for the next stage, where placeholder market data will be replaced with live sourced values.
