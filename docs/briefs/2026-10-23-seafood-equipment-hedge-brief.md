---
type: brief
engagement: fx-hedging
capability: fx-hedging
date: 2026-10-23
status: committed
hypothesis: "I expect the forward hedge to provide the strongest budget certainty because it locks the USD value of the EUR 4.7 million receivable without requiring an upfront option premium."
---
# Seafood Equipment FX Hedging Engagement Brief
Our company has invoiced a Spanish tuna canner for seafood-processing equipment and expects to receive EUR 4,700,000 in 91 days. The euro payment itself is fixed, but the amount we ultimately receive in U.S. dollars is not. If the euro weakens against the dollar before settlement, the same EUR 4.7 million receivable will convert into fewer dollars and could create a meaningful gap in expected cash flow.

The indicative 91-day forward rate is EURUSD 1.1653. At that rate, the receivable would equal approximately $5.48 million. To show the size of the exposure, if the euro were worth about 5% less at settlement, the dollar value of the receivable would fall by roughly $274,000. That potential change is large enough to affect budgeting and makes the currency exposure worth evaluating before the payment arrives.

There are three main hedge families available. A forward or futures hedge would allow the company to lock in an exchange rate today for the euros it will receive in 91 days. Its main advantage is certainty because the future USD proceeds can be known in advance. The disadvantage is that the company gives up the benefit if the euro strengthens.

A money-market hedge would use borrowing, currency conversion, and investing to create a similar fixed-dollar result using interest rates. It can provide the same type of certainty as a forward and may be useful if forward pricing is unattractive. However, it requires more transactions and uses borrowing capacity.

An option hedge would involve purchasing a put option on the euro. The provided put premium is $0.0147 per EUR, with the strike set at the spot rate. The put would establish a floor under the dollar value of the receivable while still allowing the company to benefit if the euro strengthens. The trade-off is that the premium must be paid even if the option is never exercised.

What I Am Assuming

I am assuming the EUR 4.7 million receivable will be paid in full in 91 days and that the company can access forwards, money-market borrowing and investing, and currency options. I am also assuming the quoted forward and option premium are usable for the planned hedge. USD and EUR interest rates, the current spot rate, and transaction costs will need to be verified during the later analysis.

Hypothesis

I expect the forward hedge to provide the strongest budget certainty because it locks the conversion rate for the full receivable without requiring an upfront option premium. I expect the option to provide greater upside flexibility, but at a higher cost.

How I Would Know I Was Wrong

I would reconsider this hypothesis if the money-market hedge produces a meaningfully higher guaranteed USD amount, or if the put option premium is low enough that preserving the benefit of a stronger euro provides better overall value than locking the forward rate.

Next Steps 

Stage 2 will define the workbook structure, inputs, formulas, and validation checks before the model is built. Stage 3 will use AI to build the workbook from that specification and then audit the output. Stage 4 will replace placeholders with sourced and timestamped market data. Stage 5 will independently validate the calculations and use the results to support the final hedge recommendation in a decision memo.
