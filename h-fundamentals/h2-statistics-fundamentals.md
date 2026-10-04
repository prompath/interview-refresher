[Contents](../index.md) · H2 · P1

# Statistics fundamentals

## In one minute

Statistics lets me say something about a population from a sample and state how sure I am.
The sample mean varies from sample to sample; the central limit theorem says that
variation is roughly normal with a spread that shrinks as the square root of the sample
size. Confidence intervals and hypothesis tests are both built on that.

## Key ideas

- **Distributions to know.**
  - *Bernoulli, binomial*: yes or no; number of successes in n trials.
  - *Poisson*: counts of events in a period.
  - *Normal*: sums and averages.
  - *Exponential*: waiting times.
  - *Log-normal, heavy-tailed*: revenue, usage.
- **Mean, variance, standard deviation; median and quantiles** for skewed data.
- **Standard error.** Standard deviation of an estimate: `s / sqrt(n)` for a mean,
  `sqrt(p(1−p)/n)` for a proportion.
- **Law of large numbers.** The sample mean converges to the true mean.
- **Central limit theorem.** The sample mean of independent draws is approximately normal
  for large n, whatever the underlying distribution (finite variance). Slow for very
  skewed data.
- **Confidence interval.** Estimate ± critical value × standard error.
- **Hypothesis test.** Null hypothesis, test statistic, p-value, decision at level α.
  Type I and II errors, power. See
  [A2](../a-experimentation/a2-tests-and-intervals.md).
- **Bootstrap.** Resample the data with replacement many times, recompute the statistic,
  and use the spread as its uncertainty. Works for medians, ratios and other statistics
  with no simple formula. Resample the independent unit (customers, not rows).
- **Bayes' rule.**

  ```
  P(A | B) = P(B | A) · P(A) / P(B)
  ```

  Classic use: a positive result from an accurate test for a rare condition is still
  probably a false positive, because the base rate is low.
- **Bayesian versus frequentist.** A prior updated by data to a posterior, giving direct
  probability statements about the parameter; versus long-run frequency guarantees.
- **Correlation.** Pearson (linear), Spearman (rank). Not causation; sensitive to
  outliers; zero correlation does not mean independence.
- **Covariance and variance of a sum.** `Var(X+Y) = Var(X) + Var(Y) + 2Cov(X,Y)`.
- **Maximum likelihood.** Choose parameters that make the observed data most probable;
  logistic regression is fitted this way.
- **Paradoxes.** Simpson's paradox (a trend reverses when groups are combined);
  regression to the mean (extreme values are followed by less extreme ones, which fakes
  a treatment effect when the worst cases are selected); survivorship bias.
- **Sampling.** Simple random, stratified, cluster; selection bias.

## On my CV

Under all the experimentation work. Regression to the mean and Simpson's paradox are
real risks in campaign measurement: customers are targeted because of extreme recent
behaviour.

## Likely questions

1. **Explain the central limit theorem and why it matters.** It justifies normal-based
   intervals and tests for means and rates.
2. **What is a p-value?** Probability of a result at least this extreme if the null were
   true.
3. **When would you bootstrap?** No formula for the standard error, or doubt about
   normality.
4. **A test is 99% accurate and the condition affects 1 in 1,000. Positive result?**
   About 9% chance of having it; work it through with Bayes' rule.
5. **Senior follow-up: explain a confidence interval to a marketing manager.** "Our best
   estimate is X; the data are consistent with anything from L to U."

## Pitfalls

- Standard deviation and standard error mixed up.
- Bootstrapping rows when customers have many rows.

## Sources

- Seeing Theory (visual introduction to probability and statistics): <https://seeing-theory.brown.edu/>
- OpenIntro Statistics: <https://www.openintro.org/book/os/>
- Bootstrapping (statistics): <https://en.wikipedia.org/wiki/Bootstrapping_(statistics)>
