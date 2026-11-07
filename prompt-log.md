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
