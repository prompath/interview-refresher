[Contents](../index.md) · A6 · P1

# Difference-in-differences

## In one minute

Difference-in-differences compares the change over time in a treated group with the change
in a control group. Subtracting the control's change removes anything that moved both
groups; subtracting the pre-period removes any fixed gap between them. It works when the
groups are not perfectly comparable in level, provided they would have moved in parallel
without the treatment.

## Key ideas

- **Estimator.**

  ```
  DiD = (Y_treat,post − Y_treat,pre) − (Y_ctrl,post − Y_ctrl,pre)
  ```

- **Regression form.** Same number, with standard errors and room for covariates:

  ```
  Y = β0 + β1·Treat + β2·Post + β3·(Treat × Post) + ε        effect = β3
  ```

  Cluster standard errors by customer when there are several periods per customer.
- **Parallel trends.** The identifying assumption: absent treatment, the gap between
  groups would have stayed constant. It cannot be proven, only made plausible.
- **Checking it.**
  - Plot both groups over several pre-periods.
  - *Event study*: estimate a gap for each period before and after; pre-period estimates
    should be near zero.
  - *Placebo test*: pretend the treatment started earlier; the estimate should be zero.
- **Other assumptions.** No anticipation; no other event hitting one group at the same
  time; group composition stable across periods.
- **Levels or logs.** Parallel in levels and parallel in ratios are different claims. For
  a rate or revenue with different baselines, state which one you assume.
- **Named neighbours.**
  - *CUPED*: uses pre-period outcome as a covariate to cut variance in a randomised test.
  - *Synthetic control*: builds a weighted control when there is one treated unit.
  - *Regression discontinuity*: uses a threshold rule as the source of comparison.
  - *Staggered adoption*: with different start dates, the simple two-way fixed effects
    estimate can be biased; newer estimators (Callaway and Sant'Anna) handle it.

## On my CV

"Revised uplift measurement after a mid-year change, using difference-in-differences and
A/A tests." Why it was needed: after the change the treated and control groups differed
before any treatment, so a plain post-period comparison mixed that gap with the effect.
Be ready to say what the pre-period was and how parallel trends was checked.

## Likely questions

1. **Why not just compare the groups after treatment?** That assumes the groups were equal
   before. When an A/A check shows they were not, the gap would be counted as effect.
2. **How do you defend parallel trends?** Pre-period plots, an event study with flat
   pre-period coefficients, and a placebo date.
3. **What if trends are not parallel?** Add covariates or match on pre-period behaviour,
   use a synthetic control, or report a range under stated deviations.
4. **Is DiD as good as a randomised test?** No. It rests on an untestable assumption.
   With a randomised but imbalanced split it is a correction, and a strong one.
5. **Senior follow-up: how do you explain it to the business?** "We compare how much each
   group changed, not where each ended up, so a head start by one group is not counted."

## Pitfalls

- Testing parallel trends only with a single pre-period.
- Ignoring serial correlation, which makes standard errors too small.
- Customers entering or leaving a group between periods.

## Sources

- Cunningham, *Causal Inference: The Mixtape*, Difference-in-Differences: <https://mixtape.scunning.com/08a-difference_in_differences>
- Facure, *Causal Inference for the Brave and True*, ch. 13: <https://matheusfacure.github.io/python-causality-handbook/13-Difference-in-Differences.html>
- Facure, "The Difference-in-Differences Saga" (staggered adoption): <https://matheusfacure.github.io/python-causality-handbook/24-The-Diff-in-Diff-Saga.html>
- Deng et al., CUPED (2013): <https://exp-platform.com/Documents/2013-02-CUPED-ImprovingSensitivityOfControlledExperiments.pdf>
