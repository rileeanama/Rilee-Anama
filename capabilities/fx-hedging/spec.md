University of Hawaiʻi at Mānoa · Shidler College of Business

FIN 321: International Finance and Securities

FX Transaction Hedging Project — Technical Specification

# Seafood Equipment — FX Transaction Hedge Model · Technical Specification

> Technical specification for the FX transaction hedge model — the named-range contract, calculation flow, and validation checks, precise enough that an AI or a colleague could build (or rebuild) the workbook from this document alone. This spec is the input the AI-assisted build works from.

| **Field**               | **Value** |
|-------------------------|-----------|
| **Created by**          | Rilee Anama |
| **Updated by**          | Rilee Anama |
| **Date Created**        | 2026-11-06 |
| **Date Updated**        | 2026-11-06 |
| **Version**             | 1.0 |
| **Role**                | Treasury Analyst / FP&A Analyst |
| **Audience**            | CFO / Director of Treasury |
| **Companion Workbook**  | Student build |

# FX Hedging Model Specification

## 1. Problem Statement
The company expects to receive EUR 4,700,000 from a Spanish customer in 91 days. Because the receivable is denominated in euros, the amount of U.S. dollars ultimately received depends on the EURUSD exchange rate at settlement.

The main risk is a weakening euro. If EURUSD falls before the payment is received, the same EUR 4,700,000 will convert into fewer U.S. dollars, reducing expected cash flow and potentially creating a budget shortfall.

The purpose of this model is to compare three hedging strategies — a forward hedge, a money-market hedge, and an option hedge — and show how each affects the company’s USD proceeds under different exchange-rate outcomes.

## 2. Inputs: Named-Range Contract
The workbook will use the following named ranges. Market-based values are placeholders for the model specification and are indicative, replaced with live market data at Stage 4.

Named Range

Placeholder Value

Unit

Stage 4 Source / Treatment

FC_AMT

4,700,000

EUR

Scenario value; fixed receivable amount

S0_in

1.1600

USD per EUR

Live EURUSD spot market quote

 F0_in 1.1653 USD per EUR 
Scenario-provided bank quote; retain `F0_in = 1.1653` throughout the project. If it appears inconsistent with market conditions or covered interest parity, request a requote rather than replacing it independently. |

1.1653

USD per EUR

Scenario indicative 91-day forward; verify or replace with live forward data at Stage 4

R_USD

5.30%

Annual %

Placeholder using ACT/360; replace with live U.S. interest-rate data from Federal Reserve H.15 at Stage 4

R_FC

3.10%

Annual %

Placeholder using ACT/360; replace with a live euro-area interest rate from the ECB at Stage 4

K_PUT

1.1600

USD per EUR

Set equal to S0_in; replace with an at-the-money strike based on live Stage 4 spot

K_CALL

1.1600

USD per EUR

Set equal to S0_in; replace with an at-the-money strike based on live Stage 4 spot

PREM_PUT

0.0147

USD per EUR

Scenario indicative put premium; verify or replace at Stage 4

PREM_CALL

0.0199

USD per EUR

Scenario indicative call premium; verify or replace at Stage 4

T_DAYS

91

Days

Scenario settlement period

All interest rates will use the ACT/360 convention. The spot rate, forward rate, interest rates, option strikes, and option premiums will be checked against live market data during Stage 4.

## 3. Tab Architecture
The workbook will contain the following tabs:

Cover - Provides the project title, Scenario 24 (seafood-equipment), EUR 4,700,000 exposure, 91-day settlement period, model purpose, author name (Rilee Anama), and a data-source block identifying scenario-provided inputs and Stage 4 market-data sources.

Legend/Key — Explains the workbook’s formatting, input cells, output cells, named ranges, and any color or label conventions used.

Inputs — Contains all ten named-range inputs, including the foreign-currency amount, spot rate, forward rate, interest rates, option strikes, premiums, and settlement period.

Forward Hedge — Calculates the locked USD proceeds using FC_AMT × F0_in.

Money-Market Hedge — Shows the three-step borrow, convert, and invest process using FC_AMT, R_FC, S0_in, R_USD, and T_DAYS.

Option Hedge — Calculates the put and call option outcomes across different settlement exchange rates and shows net proceeds after option premiums.

Sensitivity — Shows settlement spot rates from 0.95 × S0_in to 1.05 × S0_in in 1% steps and compares proceeds under each hedge strategy.

Notes & Assumptions — Lists the modeling assumptions, placeholder-data treatment, rate basis, transaction-cost treatment, and other limitations.

## 4. Assumptions & Constraints
The receivable amount of FC_AMT = EUR 4,700,000 is assumed to be collected in full after T_DAYS = 91.

Interest-rate calculations will use the ACT/360 convention.

The placeholder values in the specification are indicative and will be replaced with live market data at Stage 4.

Transaction costs, taxes, bid-ask spreads, and other fees are excluded from the initial model unless specifically added later.

The money-market hedge assumes the company can borrow in euros and invest in U.S. dollars at the stated placeholder rates.

The forward hedge assumes the full receivable can be hedged at F0_in.

The put and call strikes are assumed to be at-the-money, so K_PUT = S0_in and K_CALL = S0_in until live market values are used.

Option premiums are assumed to be paid at inception. Because all hedge strategies are compared at settlement in 91 days, the premium will be carried forward to settlement using R_USD and the ACT/360 convention to reflect its opportunity cost.

Covered interest rate parity is expected to make the forward hedge and money-market hedge produce approximately the same economic result, aside from rounding or market frictions.

The model is intended for comparison and decision support, not as a guarantee of future exchange-rate movements.

## 5. Calculation Flow
Forward Hedge

Calculate the locked USD proceeds as:

Forward Proceeds = FC_AMT × F0_in

This represents the amount of U.S. dollars the company would receive by selling the full EUR receivable forward at the 91-day forward rate.

Money-Market Hedge

The money-market hedge will be calculated in three separate steps so the process is visible and easy to audit.

Step 1 — Borrow EUR today

FC Borrowing = FC_AMT / (1 + R_FC × T_DAYS / 360)

This determines the amount of euros that should be borrowed today so that the loan balance at settlement equals the EUR receivable.

Step 2 — Convert the borrowed EUR to USD at spot

USD Today = FC Borrowing × S0_in

Step 3 — Invest the USD until settlement

Money-Market Proceeds = USD Today × (1 + R_USD × T_DAYS / 360)

This gives the USD value available at settlement.

Covered Interest Rate Parity Check

Calculate the implied forward rate as:

F_implied = S0_in × (1 + R_USD × T_DAYS / 360) / (1 + R_FC × T_DAYS / 360)

F_implied should be approximately equal to F0_in, allowing for differences caused by placeholder market data and rounding. Flag the model for review if ABS(F_implied - F0_in) exceeds 0.0020 USD per EUR.

Put Option Hedge

Put Premium at Settlement = FC_AMT × PREM_PUT × (1 + R_USD × T_DAYS / 360)
For each settlement spot rate S_T, calculate net proceeds as:

Put Net Proceeds = FC_AMT × MAX(S_T, K_PUT) − Put Premium at Settlement

If S_T falls below K_PUT, the put protects the company by creating a floor under the exchange rate. If S_T is above the strike, the put expires unused and the company receives the better market rate, less the premium paid.

Call Option Participation

The call option is included for comparison but is not the primary hedge for the EUR receivable because the company is exposed to a weakening euro.

For each settlement spot rate S_T, calculate the call payoff as:

Call Payoff = FC_AMT × MAX(S_T − K_CALL, 0)

Then calculate the net call payoff after the premium:

Call Premium at Settlement = FC_AMT × PREM_CALL × (1 + R_USD × T_DAYS / 360)

If S_T is below K_CALL, the call expires worthless and the premium is lost. If S_T is above K_CALL, the call gains value as the euro strengthens.

The call results should remain separate from the put hedge and the underlying receivable proceeds so the workbook does not confuse the call with the company’s primary downside-protection strategy.

## 6. Sensitivity Plan
The workbook will test how each hedge strategy performs across a range of possible EURUSD settlement rates.

The settlement spot rate, S_T, will range from:

0.95 × S0_in to 1.05 × S0_in

using 1% increments.

For each settlement rate, the workbook will calculate and compare:

Unhedged USD proceeds

Forward hedge proceeds

Money-market hedge proceeds

Put option net proceeds

Call option net proceeds

The sensitivity table will show how the company’s USD proceeds change as the euro weakens or strengthens.

The workbook will also include one comparison chart showing USD proceeds for each strategy across the full settlement-rate range.

The purpose of the chart is to help the CFO quickly see:

which strategies provide fixed or nearly fixed proceeds

which strategies protect against a weaker euro

which strategies allow participation if the euro strengthens

how the option premium affects net proceeds

The sensitivity analysis should make the trade-off between certainty, downside protection, and upside participation easy to compare.

## 7. Validation Rules
he completed workbook must pass the following checks before the results are trusted:

Forward check: Forward proceeds must equal FC_AMT × F0_in.

Money-market repayment check: The EUR amount borrowed today, grown at R_FC for T_DAYS, must equal FC_AMT at settlement.

Money-market proceeds check: The three-step borrow, convert, and invest calculation must produce the same result as the displayed money-market proceeds.

Covered interest rate parity check:
F_implied = S0_in × (1 + R_USD × T_DAYS / 360) / (1 + R_FC × T_DAYS / 360)
should be approximately equal to F0_in.

Forward vs. money-market check: Forward proceeds and money-market proceeds should be approximately equal, allowing only for rounding or market-data differences.

Put floor check: When S_T is below K_PUT, put net proceeds should not fall below the protected strike value less the premium.

Put upside check: When S_T is above K_PUT, the put should expire unused and proceeds should reflect the better market rate less the premium.

Sensitivity check: S_T must run from 0.95 × S0_in through 1.05 × S0_in in 1% increments with no missing points.

Formula check: All calculated outputs must contain formulas rather than hard-coded numbers.

Error check: No output or sensitivity-table cell may contain #VALUE!, #REF!, #DIV/0!, #N/A, or similar Excel errors.

Named-range check: All ten required named ranges must exist and be used consistently.

Input/output check: Placeholder inputs and calculated outputs must be clearly distinguished so the workbook can be reviewed and updated safely.
- **Forward check figure:** Forward proceeds must equal **$5,476,910.00** based on the current placeholder inputs. Acceptable tolerance: **±$1** for spreadsheet rounding.

- **Money-market check figure:** Money-market proceeds must equal approximately **$5,482,083.44** based on the current placeholder inputs. Acceptable tolerance: **±$1** for spreadsheet rounding.

## 8. Outputs
The workbook will produce the following summary outputs for the CFO:

Forward Proceeds — total USD proceeds from hedging the full EUR receivable at F0_in.

Money-Market Proceeds — total USD proceeds from the borrow, convert, and invest strategy.

Implied Forward Rate — the forward rate calculated from S0_in, R_USD, R_FC, and T_DAYS.

Put Net Proceeds — USD proceeds from the put hedge after deducting the option premium.

Call Net Proceeds — USD proceeds from the call comparison after deducting the option premium.

Unhedged Proceeds — USD value of the receivable at each settlement rate S_T.

Forward vs. Money-Market Difference — the difference between the two locked strategies, used as a parity and audit check.

Sensitivity Table — proceeds for each strategy across settlement rates from 0.95 × S0_in to 1.05 × S0_in.

Sensitivity Chart — one comparison chart showing how each strategy performs as EURUSD changes.

Validation Status — a summary showing whether the model passes the required checks in Section 7.

Summary output cells should be clearly identified as output cells and formatted consistently so the CFO can quickly distinguish inputs, calculations, and final results.
OUT_FWD_USD
OUT_MM_USD
OUT_F_IMPLIED
OUT_PUT_USD
OUT_CALL_USD
OUT_UNHEDGED_USD
OUT_PARITY_DIFF
OUT_VALIDATION

