[Contents](../index.md) · A4 · P1

# A/A tests

## In one minute

An A/A test splits customers the same way as an A/B test but treats both groups
identically. Any difference found is a fault in the setup, not an effect. I use it to check
that the assignment is balanced, that the metric pipeline is sound, and that the
false-positive rate is the 5% the statistics promise.

## Key ideas

- **What it validates.** Randomisation (no bias in who lands where), the metric
  computation, the variance estimate, and the absence of pre-existing differences.
- **Expected result.** About 5% of metrics significant at α = 0.05, and p-values spread
  uniformly between 0 and 1 over repeated A/A splits. Many more than 5% means the variance
  is underestimated (often correlated rows or the wrong unit of analysis).
- **Sample ratio mismatch (SRM).** Group sizes differing from the design. Test with a
  chi-square goodness-of-fit test on the counts, with a strict threshold (p < 0.001). An SRM
  means the result cannot be trusted until the cause is found.
- **Common SRM causes.** Filters applied after assignment, failed joins dropping one
  group, re-randomisation between runs, eligibility that depends on the treatment.
- **Retrospective A/A.** Re-split historical data many times in code to simulate hundreds
  of A/A tests cheaply; this gives the empirical false-positive rate.
- **Pre-period check.** Compare the groups on the outcome *before* treatment. A gap there
  is the same warning as a failed A/A.
- **Balance checks.** Compare covariates (tenure, plan, spend) across groups; standardised
  mean differences near zero.

## On my CV

"Monitored control group sampling and revised uplift measurement after a mid-year change,
using difference-in-differences and A/A tests." The story: something changed in how the
control group was drawn; an A/A style comparison showed the groups were no longer
comparable; difference-in-differences corrected for the gap. Be ready to say what the check
compared and what it showed.

## Likely questions

1. **Your A/A test is significant. What do you do?** One significant metric in twenty is
   expected. If it repeats, or the gap is large, look for SRM, assignment bugs and
   pipeline differences before running any A/B test on that split.
2. **How do you detect a sample ratio mismatch?** Chi-square test of observed counts
   against the planned ratio; investigate at p < 0.001.
3. **Groups differ before treatment. Can you still measure the effect?** Yes, by
   adjusting: difference-in-differences or a pre-period covariate (CUPED), with the
   assumptions stated. Better to fix the assignment for the next period.
4. **How often should an A/A check run?** Continuously as monitoring on a long-lived
   control group, since population drift and pipeline changes break balance over time.
5. **Senior follow-up: how would you build this into a platform?** Automatic SRM and
   pre-period balance checks on every test, alerts on failure, and results flagged as
   untrusted rather than silently reported.

## Pitfalls

- Treating a passed A/A as proof forever; balance decays.
- Fixing an SRM by trimming the larger group. The bias stays.
- Checking only group sizes, not pre-period outcomes.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*, A/A test and SRM chapters: <https://experimentguide.com/>
- Fabijan et al., "Diagnosing Sample Ratio Mismatch in Online Controlled Experiments" (2019): <https://www.researchgate.net/publication/334720020_Diagnosing_Sample_Ratio_Mismatch_in_Online_Controlled_Experiments_A_Taxonomy_and_Rules_of_Thumb_for_Practitioners>
- Lindon and Malek, automated randomisation validation and SRM detection (2022): <https://arxiv.org/pdf/2208.07766>
