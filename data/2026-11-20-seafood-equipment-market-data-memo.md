# Phase 4 Market Data Memo — Seafood Equipment FX Hedging

## Purpose

This memo documents the live market inputs used to replace the Stage 3 placeholders in the FX hedging model. Each market input includes its value, source, retrieval date, and any proxy or computation used so the analysis can be reproduced and audited.
## Market Inputs

| Input | Value Used | Source | Retrieval Date / Timestamp | Proxy / Computation Notes |
|---|---:|---|---|---|
| `S0_in` | 1.0990 USD/EUR | European Central Bank (ECB) euro reference exchange rate | 2026-11-20, ECB daily reference rate | ECB publishes currencies against the euro; EUR 1 = USD 1.0990. Used directly as the live EURUSD spot rate. |
| `R_USD` | 4.62% | Federal Reserve H.15, 1-Year Treasury Constant Maturity Rate | 2026-11-20 release; latest available market date 2026-11-19 | Used the 1-year U.S. Treasury constant maturity yield as the USD 1-year government-rate proxy because it matches the project’s 1-year rate guidance. |
| `R_FC` | 2.995% | Germany 1-Year Government Bond Yield | 2026-11-20 | Used the German 1-year government bond yield as the euro-area 1-year government-rate proxy because Germany is a major euro-area sovereign benchmark and the maturity matches the project’s 1-year rate guidance. |
| `F0_in` | 1.1653 USD/EUR | Scenario-provided bank forward quote | Original scenario quote; retained for Phase 4 | This is the bank’s quoted forward rate and is not replaced with a self-computed rate. The CIP-implied forward is calculated separately only as a cross-check. |
| `K_PUT` | 1.0990 USD/EUR | Set at live spot per scenario convention | 2026-11-20 | Strike updated to the live EURUSD spot rate used for `S0_in`. |
| `K_CALL` | 1.0990 USD/EUR | Set at live spot per scenario convention | 2026-11-20 | Strike updated to the live EURUSD spot rate used for `S0_in`. |
| `PREM_PUT` | 0.0147 USD/EUR | Scenario-provided option premium | Original scenario input; retained for Phase 4 | Scenario-given premium retained because retail-accessible option quotes are not reliable enough for this project. |
| `PREM_CALL` | 0.0199 USD/EUR | Scenario-provided option premium | Original scenario input; retained for Phase 4 | Scenario-given premium retained because retail-accessible option quotes are not reliable enough for this project. |
| `FC_AMT` | 4,700,000 EUR | Scenario-provided receivable amount | Original scenario input; retained for Phase 4 | Fixed scenario exposure; not a market-data input. |
| `T_DAYS` | 91 days | Scenario-provided settlement horizon | Original scenario input; retained for Phase 4 | Fixed scenario settlement period used in the ACT/360 calculations. |

## CIP-Implied Forward Cross-Check

Using the live market inputs:

- `S0_in = 1.0990`
- `R_USD = 4.62%`
- `R_FC = 2.995%`
- `T_DAYS = 91`

The covered interest parity formula is:

`F0 = S0 × (1 + R_USD × T/360) / (1 + R_FC × T/360)`

The resulting CIP-implied forward is:

**1.103480 USD/EUR**
The bank forward quote remains:

**1.165300 USD/EUR**

The difference between the CIP-implied forward and the bank quote is:

**1.103480 − 1.165300 = −0.061820 USD/EUR**

On the €4,700,000 receivable, this corresponds to approximately:

**−$290,552**

The negative sign means the CIP-implied forward is below the bank’s quoted forward. Because the difference exceeds the model’s parity-review tolerance, the workbook correctly flags the comparison for review. The bank quote is retained as `F0_in`; it is not replaced with the CIP-implied rate.

## Workbook Re-Check After Live Data

After replacing the Stage 3 placeholders with the live market inputs, I re-ran the workbook checks.

- Forward hedge proceeds: **$5,476,910.00**
- Money-market hedge proceeds: **$5,186,357.77**
- CIP-implied forward: **1.103480 USD/EUR**
- Forward validation check: **PASS**
- Money-market validation check: **PASS**
- Parity tolerance check: **REVIEW**
- MM vs. Forward difference check: **REVIEW**

The sensitivity table also recalculated around the new live spot rate of 1.0990, ranging from approximately 1.0441 to 1.1540, and the chart updated with the new values.

## Model Issue Found During Phase 4

Loading the live market data exposed a validation issue in the Stage 3 workbook. The money-market validation check still compared the live model output against the old placeholder check figure of $5,482,083.44, which caused the check to return FAIL even though the money-market calculation itself was correct.

I replaced the hard-coded check figure with a formula-driven validation that recomputes the expected money-market proceeds from the current named inputs. After the correction, the money-market validation check returned PASS with live proceeds of $5,186,357.77.

## FX Hedging Lab Cross-Check

I entered the same Phase 4 live inputs into the FX Hedging Lab and compared the outputs with the workbook.

- Forward hedge:
  - Lab: **$5,476,910**
  - Workbook: **$5,476,910.00**
  - Result: **Match**

- Money-market hedge:
  - Lab: **$5,186,358**
  - Workbook: **$5,186,357.77**
  - Result: **Match after rounding**

- CIP-implied forward:
  - Lab: **1.1035 USD/EUR**
  - Workbook: **1.103480 USD/EUR**
  - Result: **Match after rounding**

- Parity gap:
  - Lab: **−$290,552**
  - Workbook: **approximately −$290,552.23**
  - Result: **Match after rounding**

The FX Hedging Lab and the workbook therefore agree on the forward hedge, money-market hedge, CIP-implied forward, and parity gap. The large parity gap was not removed or forced to pass; it was retained and documented because `F0_in` remains the bank’s quoted forward rate.
