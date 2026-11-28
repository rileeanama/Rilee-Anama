# Hedge Decision Memo — Seafood Equipment

**To:** Chief Financial Officer  
**From:** Rilee Anama  
**Date:** 2026-11-27  
**Subject:** Recommendation for Hedging the €4.7 Million Receivable

## A. Exposure Summary

The company expects to receive €4,700,000 from a Spanish customer in 91 days. Because the receivable is denominated in euros, a decline in the EUR/USD exchange rate would reduce the USD value of the payment. The objective is to choose a hedge that protects the company’s expected dollar cash flow while balancing certainty, flexibility, and hedging cost.
## B. Hedge Outcomes

The forward hedge produces **$5,476,910** of guaranteed USD proceeds, the highest certain outcome among the hedging alternatives evaluated. The money-market hedge produces approximately **$5,186,358**, which is about **$290,552 less** than the bank forward quote.

At the unchanged settlement-rate baseline of `S_T = 1.0990`, remaining unhedged would produce **$5,165,300**. If the euro depreciates 5%, unhedged proceeds fall to approximately **$4,907,035**, demonstrating the downside risk of leaving the receivable exposed. If the euro appreciates 5%, unhedged proceeds rise to approximately **$5,423,565**, but this still remains below the proceeds locked in by the quoted forward.

The put option provides downside protection while preserving upside participation. After carrying the premium to settlement, the minimum protected proceeds are approximately **$5,095,403**. Under a 5% euro appreciation scenario, put proceeds increase to approximately **$5,353,668**. This flexibility comes at the cost of the option premium and produces lower proceeds than the quoted forward throughout the ±5% sensitivity range modeled.

The purchased EUR call is not a natural hedge for this EUR receivable because it benefits from euro appreciation, which already increases the USD value of the receivable. It is therefore treated as a comparison case rather than a recommended hedge.
## C. Sensitivity Interpretation

The sensitivity analysis shows a clear tradeoff between certainty and flexibility. If the euro depreciates, the unhedged position loses value immediately, while the forward and money-market hedges remain fixed. The put limits the downside by establishing a floor, but its protection is reduced by the premium cost.

If the euro appreciates, the unhedged position and put hedge both participate in the upside. The put therefore provides more flexibility than the forward, but the premium causes its net proceeds to remain below the forward throughout the modeled ±5% settlement-rate range.

The forward provides the greatest budget certainty because its proceeds do not change with the settlement exchange rate. In this scenario, it also produces more USD proceeds than the other strategies across the modeled range. The money-market hedge provides similar certainty but at a materially lower locked-in amount.
## D. Recommendation

I recommend using the **forward hedge** for the full €4,700,000 receivable, subject to confirming the bank’s quoted forward rate before execution.

The quoted forward locks in **$5,476,910**, which is higher than the money-market hedge, the put hedge, and the unhedged outcome throughout the modeled ±5% settlement-rate range. It also provides complete budget certainty without an upfront option premium.

However, the bank’s quoted forward of **1.165300 USD/EUR** does not agree with the CIP-implied forward of **1.103480 USD/EUR**. The difference is approximately **0.061820 USD/EUR**, or about **$290,552** on the €4.7 million receivable. This is a material gap.

The most likely explanation is that the government-rate proxies used for `R_USD` and `R_FC` are not the same funding and lending rates the bank would use when pricing an executable forward, although a stale or incorrect quote is also possible. Because the two supplied documents do not establish the exact cause, the bank quote should be confirmed or requoted before the hedge is executed.

This parity break does **not** change the preferred strategy based on the current model. If the quoted forward is valid and executable, it remains the strongest choice because it provides the highest certain USD proceeds and the greatest cash-flow certainty. If the bank requotes materially lower, the forward should be compared again with the money-market hedge and put before execution.
## E. Executive Justification

The forward hedge best fits the company’s need for cash-flow stability and budget certainty. It converts the uncertain euro receivable into a known USD amount without requiring an upfront premium or additional borrowing and investing transactions.

The money-market hedge also removes exchange-rate uncertainty, but it produces materially lower proceeds than the quoted forward and requires more operational steps. The put preserves upside if the euro strengthens, but that flexibility comes at a premium cost and produces lower proceeds than the forward across the modeled sensitivity range.

For this receivable, the main objective is protecting the USD value of a known future cash inflow rather than speculating on a favorable currency move. The forward therefore provides the clearest combination of certainty, simplicity, and economic value, assuming the bank confirms that the quoted rate is executable.
