[Contents](../index.md) · J3 · P1

# Experimentation strategy

## In one minute

Choosing how to measure is a senior decision. A randomised test is the default; a
long-lived holdout measures the whole programme; difference-in-differences and other
quasi-experiments are for when randomisation is impossible or has been compromised; and
attribution only shares out credit. I pick the strongest design the situation allows, say
what it assumes, and build the measurement before the thing being measured.

## Key ideas

- **Hierarchy of evidence.** Randomised experiment > quasi-experiment (DiD, regression
  discontinuity, synthetic control, instruments) > adjusted observational comparison >
  before-and-after > attribution and anecdote.
- **Choosing a design.**

  | Situation | Design |
  |---|---|
  | Can randomise customers | A/B test |
  | Need total effect of all campaigns | Global holdout |
  | Treatment already rolled out to a region or segment | Difference-in-differences, synthetic control |
  | Eligibility by a threshold | Regression discontinuity |
  | Groups imbalanced after the fact | DiD or CUPED-style adjustment |
  | Customers affect each other | Cluster randomisation |
  | Many variants, short-lived | Bandit |

- **Running many tests on one base.** Layered assignment with independent salts; mutually
  exclusive groups where treatments conflict; a shared calendar; a global holdout that
  no test may touch.
- **Variance reduction.** Pre-period covariates (CUPED), stratification, and triggered
  analysis (only customers who could have been affected) to shorten tests.
- **Long-term effects.** Short tests miss fatigue, pull-forward and churn. Keep holdouts
  and check persistence.
- **Decision rules before data.** Primary metric, guardrails, threshold for shipping,
  what happens on a null result.
- **Trust checks as standard.** Sample ratio, pre-period balance, A/A.
- **When a test cannot be run.** Too small a population, legal or fairness limits,
  one-off events. Say so, use the best quasi-experiment, and widen the stated
  uncertainty.
- **Culture.** Null and negative results reported as readily as wins; one source of truth
  for results.

## My evidence

All five measurement bullets at AIS: A/B designs, the global holdout, bucket assignment
for a vendor's tests, the difference-in-differences revision, uplift tracking.

## Likely questions

1. **How do you decide between an A/B test and difference-in-differences?** Randomise
   whenever possible; DiD when it is not, with parallel trends defended.
2. **Three teams want to test on the same customers this month.** Layering if treatments
   do not interact, exclusive groups if they do, and a power check for each.
3. **Leadership wants results faster.** Variance reduction, a bigger effect threshold, or
   leading metrics; not peeking.
4. **How would you build an experimentation practice from nothing?** Assignment service,
   standard metrics, automatic trust checks, a results log, then training.
5. **Lead-level follow-up: a senior stakeholder disputes a null result.** Show the
   interval and power, agree in advance next time on the decision rule, offer a
   replication.

## Pitfalls

- Using attribution numbers as proof of impact.
- Designing the measurement after launch.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*: <https://experimentguide.com/>
- Cunningham, *Causal Inference: The Mixtape*: <https://mixtape.scunning.com/>
- Deng et al., CUPED (2013): <https://exp-platform.com/Documents/2013-02-CUPED-ImprovingSensitivityOfControlledExperiments.pdf>
