[Contents](../index.md) · A2 · P1

# Tests and intervals for conversion

## In one minute

For conversion (yes or no per customer) I compare two proportions with a z-test, which is
the same as a 2×2 chi-square test. For revenue per customer I use Welch's t-test or a
bootstrap because the data are skewed. I report the difference with a confidence interval;
the p-value alone says nothing about size.

## Key ideas

- **Two-proportion z-test.**

  $$
  z = \frac{p_t - p_c}{\sqrt{p(1-p)\left(\frac{1}{n_t} + \frac{1}{n_c}\right)}} \qquad p = \text{pooled rate}
  $$

- **Interval for the absolute difference** uses the unpooled standard error:

  $$
  (p_t - p_c) \pm 1.96 \sqrt{\frac{p_t(1-p_t)}{n_t} + \frac{p_c(1-p_c)}{n_c}}
  $$

- **Interval for relative uplift** `p_t/p_c − 1`. The ratio is not normal, so work on the
  log scale (delta method) and transform back, or bootstrap:

  $$
  \operatorname{Var}\left(\ln\frac{p_t}{p_c}\right) \approx \frac{1-p_t}{n_t\,p_t} + \frac{1-p_c}{n_c\,p_c}
  $$

  A small control group makes this interval wide and lopsided.
- **Chi-square test.** For two groups it gives z². For more than two groups it is the
  omnibus test. Use Fisher's exact test when expected counts are below about five.
- **Welch's t-test.** Means with unequal variances; safe default for revenue. With heavy
  tails, large n is needed for the normal approximation, so check with a bootstrap.
- **p-value.** The probability of data at least this extreme if there were no effect. Not
  the probability that the null is true.
- **Type I error (α)**: declaring an effect that is not there. **Type II (β)**: missing one
  that is. Power = 1 − β.
- **Statistical versus practical significance.** A huge sample makes a trivial effect
  significant; a small one hides a real effect.

## On my CV

Behind "the outbound model showed +53% to +77% conversion uplift in most months": be able to
say how the uplift and its uncertainty were computed and why some months were not
significant (see [A7](a7-uplift-measurement.md)).

## Likely questions

1. **z-test or t-test for conversion?** z-test; with large n they agree. The t-test is for
   means of continuous outcomes.
2. **What does a 95% confidence interval mean?** If the experiment were repeated many
   times, 95% of such intervals would contain the true value. It is not a 95% probability
   for this one interval, though that is how it is used in practice.
3. **How do you get an interval for a percentage uplift?** Delta method on the log ratio,
   or bootstrap customers within each group and take percentiles.
4. **Revenue is zero for most customers and huge for a few. What do you do?** Welch or
   bootstrap on the mean, since the business cares about the total; consider capping
   outliers as a sensitivity check and say so.
5. **Senior follow-up: one-sided or two-sided?** Two-sided by default. One-sided only when
   a harmful result and a null result lead to the same decision, and decided beforehand.

## Pitfalls

- Reporting relative uplift without the baseline: +60% of a very small rate is small.
- Using the pooled standard error for the confidence interval.
- Treating repeated measures per customer as independent rows.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*, statistics chapters: <https://experimentguide.com/>
- Larsen et al., "Statistical Challenges in Online Controlled Experiments" (2023): <https://www.tandfonline.com/doi/full/10.1080/00031305.2023.2257237>
- Zhou et al., "All about sample-size calculations for A/B testing" (2023): <https://arxiv.org/pdf/2305.16459>
