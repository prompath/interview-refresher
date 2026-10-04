[Contents](../index.md) · A9 · P2

# Multi-touch attribution

## In one minute

Attribution divides credit for a conversion among the marketing touches that preceded it.
Rule-based models use a fixed rule (last touch, first touch, linear). Data-driven models
(Markov chains, Shapley values) estimate each channel's contribution from the observed
paths. All of them redistribute conversions that happened; none shows how many would have
happened with no marketing, which is why attribution is paired with a holdout.

## Key ideas

- **Rule-based.** Last touch, first touch, linear, time decay, position-based. Simple and
  arbitrary; last touch over-credits channels near the purchase.
- **Markov chain attribution.**
  - Each channel is a state, plus Start, Conversion and Null (no conversion).
  - Transition probabilities are estimated from customer journeys.
  - **Removal effect** of a channel: the share of conversions lost if that channel is
    removed (its transitions redirected to Null).
  - Credit = the channel's removal effect divided by the sum of all removal effects.
  - First-order chains use only the previous touch; higher orders capture sequences but
    need far more data.
- **Shapley value.** Each channel's average marginal contribution over all orderings of
  channels. Fair by construction, expensive with many channels.
- **Limits.** Observational: channels are targeted at likely buyers, so correlation with
  conversion is not causation. Journeys are incomplete (offline touches, untracked
  channels). Results depend on the lookback window and path definition.
- **Attribution and incrementality together.** The holdout gives the total incremental
  effect; attribution shares that total among channels. Attribution alone can credit
  channels for organic conversions.
- **Marketing mix modelling.** The aggregate alternative: regress outcomes on spend by
  channel over time; no customer-level paths needed.

## On my CV

"Implemented the global control group holdout for a vendor multi-touch attribution
project." The vendor built the attribution; my part was the holdout that calibrates it.
Do not name the vendor. Know Markov attribution well enough to explain why the holdout
was needed.

## Likely questions

1. **Why is last touch misleading?** It credits the channel closest to purchase, often one
   that reaches customers already about to buy.
2. **Explain the removal effect.** Remove a channel from the chain, recompute the
   probability of reaching Conversion, and take the relative drop.
3. **Markov or Shapley?** Markov respects order and scales to many channels; Shapley has
   cleaner fairness properties but ignores order and grows exponentially.
4. **Does attribution measure incrementality?** No. It allocates observed conversions. A
   randomised holdout measures the increment.
5. **Senior follow-up: attribution and the holdout disagree.** Trust the experiment for
   the total and use attribution for relative shares; investigate channels where the gap
   is largest with channel-level holdouts.

## Pitfalls

- Presenting attribution shares as causal effects.
- Ignoring non-converting paths; the Markov model needs them.

## Sources

- Bryl, "Marketing Multi-Channel Attribution model (Markov chains concept)": <https://www.analyzecore.com/2016/08/03/attribution-model-r-part-1/>
- Databricks, "Multi-Touch Attribution Model Solution": <https://www.databricks.com/blog/2021/08/23/solution-accelerator-multi-touch-attribution.html>
- Causality Engine, "Markov Chain Attribution Explained: How It Works and Where It Misleads": <https://www.causalityengine.ai/resources/markov-chain-attribution-explained>
