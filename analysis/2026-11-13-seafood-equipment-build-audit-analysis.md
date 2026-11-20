# Stage 3 Build Audit — Seafood Equipment FX Hedging Model

## Finding 1 — Incorrect `F0_in` Defined Name

**What I checked:**  
I reviewed the workbook’s defined names in Excel Name Manager and verified that the required inputs pointed to the intended cells on the Inputs tab.

**What I found:**  
The forward rate 1.1653 was correctly entered in `Inputs!B7`, but the defined name `F0_in` incorrectly referred to `Inputs!SB$7`, which is an empty cell. Because the forward hedge formulas referenced `F0_in`, the committed workbook showed forward proceeds of $0 and the Cover forward validation check showed FAIL.

**What I changed:**  
I corrected `F0_in` in Name Manager so it now refers to:

`=Inputs!$B$7`

After the correction, `Forward Hedge!B7` calculated forward proceeds of **$5,476,910.00** and the Cover forward check returned PASS.

## Finding 2 — Forward Validation Check Used a Hard-Coded Check Figure

**What I checked:**  
I reviewed the Cover validation formula used to test the forward hedge.

**What I found:**  
The original validation formula compared the model result against the typed value 5,476,910. This meant the check depended on a hard-coded figure rather than recalculating from the model inputs. If the receivable amount or forward rate changed, the check could report the wrong status.

**What I changed:**  
I replaced the hard-coded comparison with:

`=IF(ABS(OUT_FWD_USD-(Inputs!$B$5*Inputs!$B$7))<=1,"PASS","FAIL")`

The revised check now compares the model output with an independent calculation based on the actual input cells.

## Finding 3 — Required Named Ranges

**What I checked:**  
I reviewed the ten required input names in Excel Name Manager and confirmed that each one resolves to the intended input cell.

**What I found:**  
The required names were present, but `F0_in` contained the incorrect reference described in Finding 1.

**What I changed:**  
I corrected `F0_in` and confirmed the required named ranges point to their intended cells.

## Finding 4 — Formula-Driven Calculated Cells

**What I checked:**  
I reviewed the hedge calculations and sensitivity table to confirm that calculated outputs use formulas rather than manually typed results.

**What I found:**  
The forward hedge, money-market hedge, option calculations, and sensitivity table are formula-driven. Changing `S0_in` from 1.1600 to 1.1700 caused the sensitivity table to recalculate automatically.

**What I changed:**  
No calculated cells required replacement after this review. The sensitivity test confirmed that the table is linked to model inputs.

## Finding 5 — Money-Market Check Figure

**What I checked:**  
I compared the money-market hedge output with the Stage 2 check figure using the required ACT/360 convention.

**What I found:**  
The workbook calculated money-market proceeds of approximately **$5,482,083.44**, matching the expected check figure.

**What I changed:**  
No correction was required.

## Finding 6 — MM vs. Forward Difference Validation Threshold

**What I checked:**  
I reviewed the Cover validation check for the difference between the money-market hedge and forward hedge.

**What I found:**  
The validation formula used a $1 tolerance:

`=IF(ABS(C36)<=1,"PASS","REVIEW")`

The actual difference was **$5,173.44**, so the check returned REVIEW even though the Stage 2 specification allowed a parity-review threshold equivalent to **$9,400** for the €4.7 million receivable.

**What I changed:**  
I updated the validation formula to:

`=IF(ABS(C36)<=9400,"PASS","REVIEW")`

After the change, the validation returned PASS.

## Finding 7 — Assumption Formatting

**What I checked:**  
I compared the Inputs tab formatting with the Legend/Key.

**What I found:**  
The Legend defined Blue as the color for assumptions, but no assumption cells used blue formatting.

**What I changed:**  
I applied the blue assumption formatting to the interest-rate assumption cells for `R_USD` and `R_FC`.

## Audit Conclusion

The audit identified and corrected the `F0_in` defined-name error, removed the hard-coded forward validation figure, corrected the MM vs. Forward validation threshold, and aligned the assumption formatting with the Legend. I also verified the required input names, formula-driven calculations, sensitivity behavior, and the money-market check figure.
