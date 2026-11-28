Independent FX Transaction Hedge Analysis — Seafood Equipment
1. Objective and model inputs
Seafood Equipment expects to receive €4,700,000 from a Spanish customer in 91 days. Because the receivable is denominated in euros, the company faces transaction exposure arising from fluctuations in the EUR/USD exchange rate. A depreciation of the euro would reduce the USD value of the receivable.

The objective is to evaluate the available hedging strategies and recommend the alternative that best protects the company's USD cash flows.

This analysis uses only the supplied Technical Specification and Phase 4 Market Data Memo. All results are recomputed directly from the documented inputs and formulas without accessing the workbook or prior project work.
Named input	Value	Unit
FC_AMT	4,700,000	EUR
S0_in	1.0990	USD/EUR
F0_in	1.1653	USD/EUR
R_USD	4.62%	Annual rate
R_FC	2.995%	Annual rate
K_PUT	1.0990	USD/EUR
K_CALL	1.0990	USD/EUR
PREM_PUT	0.0147	USD/EUR
PREM_CALL	0.0199	USD/EUR
T_DAYS	91	Days


The ACT/360 time fraction is:

\[ t=\frac{91}{360}=0.252777778 \]

The corresponding interest accumulation factors are:

\[ 1+R_{USD}t=1.011678333 \]

\[ 1+R_{FC}t=1.007570694 \]

Calculations retain full precision until final presentation.
2. Forward hedge
The company enters into a forward contract to sell the entire €4,700,000 receivable at the bank's quoted 91-day forward rate.

Formula:

\[ \text{Forward proceeds}=FC\_AMT\times F_0 \]

Calculation:

\[ =4,700,000\times1.1653 \]

\[ \boxed{\$5,476,910.00} \]

The forward hedge eliminates exchange-rate uncertainty by locking in the USD proceeds at settlement, assuming the quoted rate is executable.
Forward hedge component	Result
EUR sold forward	€4,700,000.00
Contracted exchange rate	1.165300
Locked USD proceeds	$5,476,910.00


3. Money-market hedge
The money-market hedge involves borrowing euros today, converting the borrowed euros into USD, and investing the USD until the receivable is collected.
Step 1 — Borrow euros today
Calculate the present value of the EUR receivable using the euro interest rate.

\[ \text{EUR borrowing}= \frac{FC\_AMT}{1+R_{FC}t} \]

\[ =\frac{4,700,000} {1+0.02995(91/360)} \]

\[ \boxed{€4,664,685.09} \]

The EUR loan will accumulate to €4,700,000 at settlement.
Step 2 — Convert borrowed euros into USD
Convert the borrowed euros at the current spot exchange rate.

\[ \text{USD today}=\text{EUR borrowing}\times S_0 \]

\[ =4,664,685.094470\times1.0990 \]

\[ \boxed{\$5,126,488.92} \]
Step 3 — Invest USD until settlement
Invest the USD proceeds for 91 days at the USD interest rate.

\[ \text{MM proceeds}=\text{USD today}(1+R_{USD}t) \]

\[ =5,126,488.918823 [1+0.0462(91/360)] \]

\[ \boxed{\$5,186,357.77} \]
Money-market hedge cash flow summary
Transaction	Amount
EUR borrowed today	€4,664,685.09
EUR interest expense	€35,314.91
EUR loan repayment at settlement	€4,700,000.00
USD invested today	$5,126,488.92
USD interest earned	$59,868.85
Final USD proceeds	$5,186,357.77


At settlement, the customer's €4,700,000 payment fully repays the EUR loan. The company retains the accumulated USD investment.
4. Covered interest parity (CIP)
Covered interest parity establishes the theoretical forward exchange rate implied by the current spot exchange rate and the interest-rate differential between the two currencies.

Formula:

\[ F_{\text{implied}}= S_0\frac{1+R_{USD}t}{1+R_{FC}t} \]

Calculation:

\[ =1.0990 \frac{1+0.0462(91/360)} {1+0.02995(91/360)} \]

\[ \boxed{1.103480376\text{ USD/EUR}} \]
Comparison with the bank forward quote
\[ \text{Parity difference}=F_{\text{implied}}-F_0 \]

\[ =1.103480376-1.165300 \]

\[ =-0.061819624\text{ USD/EUR} \]

The dollar impact of the parity difference is:

\[ 4,700,000(-0.061819624) \]

\[ \boxed{-\$290,552.23} \]
Covered interest parity validation
Bank forward quote
1.165300
CIP-implied forward
1.103480
Absolute parity difference

0.061820

Specification tolerance

0.002000

Amount exceeding tolerance

0.059820

Validation status

REVIEW

The absolute parity difference is approximately 30.91 times the permitted tolerance. The bank forward quote produces $290,552.23 more than the money-market hedge.

The discrepancy is material and requires investigation. However, the technical specification explicitly requires retaining the scenario-provided bank quote rather than replacing it with the CIP-implied forward rate.

The government interest-rate proxies may contribute to the discrepancy, but the two documents do not establish its exact cause. A bank requote or confirmation is necessary before execution.
5. Unhedged position
If the company remains unhedged, the entire EUR receivable is converted into USD at the prevailing exchange rate on the settlement date.

Formula:

\[ \text{Unhedged proceeds}=FC\_AMT\times S_T \]

Because the future settlement exchange rate is unknown, the current spot rate is used as the unchanged-rate baseline.

\[ =4,700,000\times1.0990 \]

\[ \boxed{\$5,165,300.00} \]
Settlement scenario	Exchange rate	USD proceeds
Euro depreciates 5%	1.04405	$4,907,035.00
Euro remains unchanged	1.09900	$5,165,300.00
Euro appreciates 5%	1.15395	$5,423,565.00


A 5% depreciation of the euro would reduce USD proceeds by $258,265 relative to the unchanged-rate baseline.

Remaining unhedged provides full upside participation but no protection against euro depreciation.
6. Put option hedge
The company purchases a EUR put option that provides the right, but not the obligation, to sell euros at the strike price of 1.0990 USD/EUR.
Step 1 — Calculate the initial premium
\[ \text{Initial premium}=FC\_AMT\times PREM\_PUT \]

\[ =4,700,000\times0.0147 \]

\[ =\$69,090.00 \]
Step 2 — Carry the premium forward to settlement
\[ \text{FV of premium}=69,090[1+0.0462(91/360)] \]

\[ \boxed{\$69,896.86} \]
Step 3 — Calculate net settlement proceeds
\[ \text{Put net proceeds}= FC\_AMT\max(S_T,K_{PUT})-\text{FV of premium} \]

When the settlement exchange rate is below the strike, the company exercises the option. When the settlement exchange rate is above the strike, the option expires unused and the company converts the receivable at the more favorable market rate.
Minimum protected proceeds
\[ =4,700,000(1.0990)-69,896.85605 \]

\[ \boxed{\$5,095,403.14} \]
Put option component	Result
Strike price	1.099000
Initial premium	$69,090.00
Premium opportunity cost	$806.86
Settlement-adjusted premium	$69,896.86
Minimum net proceeds	$5,095,403.14
Effective minimum exchange rate	1.084128


The put establishes a minimum level of USD proceeds while preserving the ability to benefit from euro appreciation, net of the premium.
7. Call option payoff and net result
The EUR call option provides the right to purchase euros at the strike price. Because the company already expects to receive euros, a purchased call does not directly protect the receivable against euro depreciation.
Step 1 — Calculate the initial premium
\[ \text{Initial premium}=4,700,000\times0.0199 \]

\[ =\$93,530.00 \]
Step 2 — Carry the premium forward to settlement
\[ \text{FV of premium}=93,530[1+0.0462(91/360)] \]

\[ \boxed{\$94,622.27} \]
Step 3 — Calculate gross and net call payoff
\[ \text{Call payoff}=FC\_AMT\max(S_T-K_{CALL},0) \]

\[ \text{Net call payoff}= FC\_AMT\max(S_T-K_{CALL},0)-94,622.274517 \]
Settlement scenario	Gross call payoff	Net call payoff
Euro depreciates 5%	$0.00	−$94,622.27
Euro remains unchanged	$0.00	−$94,622.27
Euro appreciates 5%	$258,265.00	$163,642.73


Call break-even exchange rate
\[ S_T=K_{CALL}+\frac{\text{FV of premium}}{FC\_AMT} \]

\[ =1.0990+\frac{94,622.274517}{4,700,000} \]

\[ \boxed{1.119132399\text{ USD/EUR}} \]

The euro must appreciate approximately 1.83% from the current spot rate for the standalone call option to generate a positive net payoff.

The call results are reported separately from the underlying receivable proceeds, consistent with the technical specification.
8. Complete sensitivity analysis
The specification requires settlement exchange rates ranging from 95% to 105% of the current spot exchange rate, using 1% increments.

\[ S_T=S_0(1+\text{percentage change}) \]

Lower bound:

\[ 1.0990(0.95)=1.04405 \]

Upper bound:

\[ 1.0990(1.05)=1.15395 \]
Receivable proceeds by hedging strategy
All monetary values are in USD.
Spot change	Settlement rate	Unhedged	Forward	Money market	Net put
−5%	1.04405	4,907,035.00	5,476,910.00	5,186,357.77	5,095,403.14
−4%	1.05504	4,958,688.00	5,476,910.00	5,186,357.77	5,095,403.14
−3%	1.06603	5,010,341.00	5,476,910.00	5,186,357.77	5,095,403.14
−2%	1.07702	5,061,994.00	5,476,910.00	5,186,357.77	5,095,403.14
−1%	1.08801	5,113,647.00	5,476,910.00	5,186,357.77	5,095,403.14
0%	1.09900	5,165,300.00	5,476,910.00	5,186,357.77	5,095,403.14
+1%	1.10999	5,216,953.00	5,476,910.00	5,186,357.77	5,147,056.14
+2%	1.12098	5,268,606.00	5,476,910.00	5,186,357.77	5,198,709.14
+3%	1.13197	5,320,259.00	5,476,910.00	5,186,357.77	5,250,362.14
+4%	1.14296	5,371,912.00	5,476,910.00	5,186,357.77	5,302,015.14
+5%	1.15395	5,423,565.00	5,476,910.00	5,186,357.77	5,353,668.14
