[Contents](../index.md) · A1 · P1

# A/B test design

## In one minute

An A/B test randomly splits units (customers) into groups that differ in one thing, so any
difference in the outcome beyond chance is caused by that thing. Before launch I fix the
hypothesis, the randomisation unit, one primary metric, the guardrail metrics, the smallest
effect worth detecting, and from those the sample size and duration. After launch I check
the split is what I asked for, then analyse once, at the planned end.

## Key ideas

- **Randomisation unit.** Usually the customer, not the call or the session. The unit of
  analysis should match it, or the observations are not independent.
- **Primary metric.** One metric decides the test. Guardrails (churn, complaints, opt-outs)
  can veto a win but do not declare one.
- **Power and sample size.** For two conversion rates, per group:

  $$
  n \approx \frac{2\,(z_{\alpha/2} + z_{\beta})^2 \; p(1-p)}{\delta^2}
  $$

  $$
  n \approx \frac{16\, p(1-p)}{\delta^2} \qquad (\alpha = 0.05 \text{ two-sided, power } = 80\%)
  $$

  $$p$$ is the baseline rate and $$\delta$$ the absolute minimum detectable effect. Halving
  $$\delta$$ quadruples $$n$$.
- **Duration.** Long enough to reach $$n$$ and to cover whole cycles (a billing cycle in
  telecom, at least full weeks elsewhere).
- **Peeking.** Checking daily and stopping at the first p < 0.05 inflates false positives
  well above 5%. Either fix the horizon or use a sequential method (alpha spending,
  always-valid p-values).
- **Novelty and primacy.** Early effects can fade or grow; plot the effect over time.
- **Interference.** The stable unit assumption fails when one customer's treatment affects
  another (shared family plans, a limited call-centre capacity shared by arms).
- **Unequal splits.** A small control costs less revenue but has less power; power is
  driven by the smaller group.

## On my CV

"Designed A/B experiments, including a four-arm right-time-to-call test and a reinforcement
learning offer model against a monthly one." Be ready to walk through one design end to
end: unit, arms, metric, size, duration, and what was decided from the result.

## Likely questions

1. **How do you choose the sample size?** From the baseline rate, the minimum effect the
   business would act on, α and power. If the required size is more than the eligible base,
   I say so and either lengthen the test, accept a larger detectable effect, or use a
   variance reduction method.
2. **The test is not significant. What now?** Report the interval, not just "no effect".
   If the interval excludes effects large enough to matter, that is a useful result; if it
   is wide, the test was underpowered.
3. **Why not stop early when it looks good?** Repeated looks give many chances to cross the
   threshold by luck. Stop early only with a pre-planned sequential rule.
4. **What can go wrong in the split?** Sample ratio mismatch, eligibility filters applied
   after assignment, customers switching groups, treatment not delivered (call not
   answered). The last one is why I analyse by assigned group (intention to treat).
5. **Senior follow-up: the business wants a decision in two weeks but the test needs
   eight.** Offer choices with their risks: a larger detectable effect, a leading metric
   with a known link to the real one, or a decision now with a holdout kept to measure it
   afterwards.

## Pitfalls

- Picking the metric after seeing the data.
- Analysing only customers who were reached. That breaks randomisation.
- Treating "p > 0.05" as "no effect".

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments* (2020): <https://experimentguide.com/>
- Evan Miller, sample size calculator: <https://www.evanmiller.org/ab-testing/sample-size.html>
- Evan Miller, "How Not To Run an A/B Test" (peeking): <https://www.evanmiller.org/how-not-to-run-an-ab-test.html>
- Larsen et al., "Statistical Challenges in Online Controlled Experiments" (2023): <https://www.tandfonline.com/doi/full/10.1080/00031305.2023.2257237>
