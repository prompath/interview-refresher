[Contents](../index.md) · A10 · P2

# Testing an adaptive model

## In one minute

Comparing a model that learns continuously (a bandit or reinforcement learning policy)
with a monthly batch model is still an A/B test: randomise customers between the two
*policies* and compare outcomes. The differences are that the adaptive arm changes during
the test, needs a warm-up, and must learn only from its own customers.

## Key ideas

- **Randomise the policy, not the offer.** Each customer is assigned to a policy for the
  whole test; the unit of comparison is the policy's total result.
- **Learning period.** The adaptive policy starts poorly and improves. Decide beforehand
  whether the comparison includes the warm-up (cost of adoption) or starts after it
  (steady state). Report both if possible.
- **No leakage between arms.** The adaptive model must update only on feedback from its
  own arm; otherwise the arms are not independent.
- **Exploration cost.** A bandit deliberately makes some sub-optimal offers. A fair
  comparison includes that cost.
- **Cadence mismatch.** Daily decisions against monthly ones: align the window (same
  customers, same calendar period, same opportunities to offer) and the metric
  (conversion or revenue per customer per period, not per offer).
- **Non-stationarity.** Promotions and seasonality change during the test. Running both
  arms at the same time handles it; comparing before and after does not.
- **A random arm.** A third group with random offers gives a floor and unbiased data for
  later off-policy evaluation.
- **Metric horizon.** An adaptive policy may win on short-term conversion but push
  cheaper offers. Track revenue and a guardrail (churn, downgrades).
- **Off-policy evaluation (by name).** Estimating a new policy's value from logged data of
  an old one, using inverse propensity weighting. Needs logged probabilities of each
  action.

## On my CV

"Designed A/B experiments, including ... a reinforcement learning offer model against a
monthly one." Be ready to state the unit, the window, the metric, and how the warm-up was
handled. The model itself I maintain and did not build.

## Likely questions

1. **How is this different from a normal A/B test?** One arm is a moving target; I compare
   policies over a window instead of fixed treatments.
2. **When do you start measuring?** Pre-declare a warm-up, or measure cumulative from day
   one and show the trend.
3. **Why keep a random group?** Baseline, and clean data to evaluate future policies
   offline.
4. **The adaptive model wins on conversion and loses on revenue. Verdict?** It optimised
   the reward it was given. Fix the reward (revenue or margin) before deciding.
5. **Senior follow-up: is the complexity worth it?** Only if the gain over the batch model
   exceeds the cost of daily pipelines, monitoring and harder debugging.

## Pitfalls

- Comparing the adaptive model's later months with the batch model's earlier months.
- Letting both arms train on pooled feedback.

## Sources

- Multi-armed bandit: <https://en.wikipedia.org/wiki/Multi-armed_bandit>
- Li et al., "A Contextual-Bandit Approach to Personalized News Article Recommendation" (2010; LinUCB and offline evaluation): <https://arxiv.org/abs/1003.0146>
- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*: <https://experimentguide.com/>
