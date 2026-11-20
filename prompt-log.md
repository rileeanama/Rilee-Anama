# Prompt Log

This file keeps a record of important AI prompts used to help build and maintain this portfolio repository.

## Setup Prompts

### Portfolio Repository Setup
Prompt used to help create the repository structure and supporting files such as `AGENTS.md`, `CLAUDE.md`, `.gitignore`, and project folders.

### Resume Update
Prompt used to update and format `RESUME.md` using current work experience, education, and skills.

### Bio Update
Prompt used to draft and revise the bio in `README.md` so it sounds natural, professional, and reflects my background.

## Future Prompts

Add new prompts below as AI is used for future projects, analysis, writing, coding, or portfolio updates.

## 2026-10-30

### Prompt
Help me understand and complete Stage 1 of my FX hedging project for Scenario 24, seafood-equipment. My scenario has a EUR 4,700,000 receivable due in 91 days, an indicative forward rate of 1.1653, and an EUR put premium of $0.0147 per EUR.

### Purpose
Used AI to interpret the Stage 1 requirements, organize the executive brief, explain the exposure and hedge alternatives, and help place the files in the correct GitHub folders.

## 2026-11-06

### Prompt
Review my Stage 2 FX hedging model specification and identify specific gaps or ambiguities that could cause an AI to build the workbook incorrectly.

### AI Review Finding
The review found that my draft clearly specified the put option payoff but did not define the call option treatment with the same level of precision. The assignment says to specify the call participation payoff, so leaving it vague could cause the Stage 3 workbook to implement the wrong formula.

### Fix
Before: The draft included a call net proceeds formula without clearly explaining how the call should be used or interpreted in the model.

After: I clarified that the call result is included as a separate comparison output and should not be confused with the main hedge for the EUR receivable. I also kept the put as the primary option hedge because the firm is receiving EUR and needs protection against EUR weakness.

### Purpose
This iteration made the specification more precise so the Stage 3 AI build has less room to guess.
### Specific Iteration

**Before:** My original Section 5 treated the call option too much like another hedge on the receivable and used a formula that did not clearly separate the call payoff from the receivable proceeds.

**AI Review Finding:** The call option treatment was ambiguous and could cause the Stage 3 workbook to build the wrong payoff logic.

**After:** I revised Section 5 so the put remains the main option hedge for the EUR receivable, while the call is shown separately as a comparison. The revised section now uses:

`Call Payoff = FC_AMT × MAX(S_T − K_CALL, 0)`

and

`Call Net Payoff = FC_AMT × MAX(S_T − K_CALL, 0) − FC_AMT × PREM_CALL`

This change makes the model logic clearer and reduces the chance that the Stage 3 build will confuse the call with the company’s primary hedge.

## 2026-11-13

### Prompt
Help me revise my Stage 2 FX hedging model specification using my professor’s feedback. I need to fix the treatment of the option premium, add numerical check figures and tolerances to Section 7, define what “material” means for the parity check, keep the given forward rate instead of replacing it in Stage 4, name the Section 8 outputs, and finish the Cover tab description.

### Purpose
Used AI to help interpret the professor’s review and make the Stage 2 specification more precise and auditable before the Stage 3 workbook build.

### Specific Fixes Made
- Updated `F0_in` so the scenario-provided bank forward quote of 1.1653 is retained throughout the project unless a requote is requested.
- Added numerical validation check figures for forward proceeds and money-market proceeds.
- Added a specific parity tolerance of `0.0020 USD per EUR` instead of using the vague word “material.”
- Clarified that option premiums are paid at inception and should be carried forward to settlement using `R_USD` and ACT/360 when comparing day-91 proceeds.
- Added exact named ranges for summary outputs in Section 8.
- Added the author and data-source block requirements to the Cover tab description.

### Result
The revised specification gives the Stage 3 builder exact numbers, tolerances, and output names to check against, reducing ambiguity in the workbook build and audit.

## 2026-11-13

### Prompt
Build and audit Stage 3 of my FX hedging project using the committed Stage 2 specification at `capabilities/fx-hedging/spec.md`. The workbook must include all required tabs, formulas, hedge calculations, sensitivity analysis, validation checks, and the required named ranges.

### Purpose
Used AI to help generate the workbook structure from the Stage 2 specification and guide the audit process before submission.

### Build and Audit Notes
- Saved the completed workbook as `capabilities/fx-hedging/model.xlsx`.
- Added the ten required input named ranges in Excel and confirmed the `#NAME?` errors disappeared.
- Added the summary output named ranges required by the Stage 2 specification.
- Tested the sensitivity table by changing `S0_in` from 1.1600 to 1.1700 and confirmed the table recalculated automatically.
- Confirmed forward proceeds equal $5,476,910.00.
- Confirmed money-market proceeds equal approximately $5,482,083.44.
- Documented the audit findings in `analysis/2026-11-13-seafood-equipment-build-audit-analysis.md`.

### Result
The workbook passed the tested validation checks and the audit note documents the checks performed before submission.

## 2026-11-20

### Prompt
Review the Stage 3 grader feedback and correct the FX hedging workbook, audit note, and specification before beginning Stage 4.

### Purpose
Used AI to help interpret the grader feedback, identify the specific Stage 3 defects, and guide the corrections one at a time.

### Corrections Made
- Corrected the defined name `F0_in` so it refers to `=Inputs!$B$7`.
- Confirmed the forward hedge now calculates $5,476,910.00.
- Replaced the hard-coded forward validation check with a formula-driven check using the workbook inputs.
- Updated the MM vs. Forward validation threshold to $9,400 based on the Stage 2 parity threshold.
- Applied Blue formatting to the USD and EUR interest-rate assumption cells to match the Legend/Key.
- Revised the Stage 3 audit note to document the actual defects found, the corrections made, the named-range review, and the formulas-only review.
- Updated `spec.md` to clarify that the scenario-provided bank forward quote remains `F0_in` at Stage 4 unless a requote is requested.

### Result
The Stage 3 workbook and documentation were corrected to address the grader feedback before continuing to Stage 4.

## 2026-11-20

### Prompt
Use the Stage 4 FX hedging instructions to replace the workbook placeholders with live market data, document the provenance of each input, compute the CIP-implied forward, re-run the workbook checks, and cross-check the model against the FX Hedging Lab.

### Purpose
Used AI to help identify appropriate live market sources, enter the Phase 4 inputs step by step, verify the workbook outputs, document the market-data provenance, and compare the workbook with the course FX Hedging Lab.

### Live Data and Model Updates
- Updated `S0_in` to 1.0990 USD/EUR using the ECB reference rate.
- Updated `R_USD` to 4.62% using the Federal Reserve H.15 1-year Treasury constant maturity rate.
- Updated `R_FC` to 2.995% using the Germany 1-year government bond yield as the euro-area proxy.
- Kept the scenario bank forward quote `F0_in = 1.1653`.
- Updated `K_PUT` and `K_CALL` to the live spot rate of 1.0990.
- Retained the scenario option premiums of 0.0147 and 0.0199.
- Confirmed the CIP-implied forward of approximately 1.103480 USD/EUR.
- Documented the parity difference of approximately −0.061820 USD/EUR, or about −$290,552 on the €4.7 million receivable.
- Fixed the money-market validation check so it recomputes from the current live inputs rather than comparing against the Stage 3 placeholder check figure.
- Confirmed the sensitivity table and chart recalculated around the live spot rate.
- Cross-checked the workbook against the FX Hedging Lab and confirmed the forward hedge, money-market hedge, CIP-implied forward, and parity gap matched after rounding.

### Result
The Phase 4 workbook was populated with live market inputs, the market-data memo was completed in the `data` folder, the validation issue exposed by the live data was corrected, and the workbook matched the FX Hedging Lab cross-check.
