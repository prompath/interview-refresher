[Contents](../index.md) · A7 · P1

# Uplift measurement

## In one minute

Uplift is the difference between what treated customers did and what they would have done
anyway, estimated from a randomised control group. I measure it per period as incremental
conversions and incremental revenue per customer (ARPU), each with an interval, and I
separate two questions: does the *campaign* work (treated versus no contact) and does the
*model* work (model-targeted versus randomly targeted).

## Key ideas

- **Absolute and relative uplift.**

  ```
  absolute  = r_t − r_c
  relative  = r_t / r_c − 1
  incremental conversions = (r_t − r_c) · N_t
  ```

- **ARPU uplift.** Difference in mean revenue per customer between groups, over *all*
  assigned customers, not only converters. Revenue is skewed, so use Welch or a bootstrap.
- **Two baselines.**
  - *No-contact control*: the effect of contacting at all.
  - *Random-targeting control*: same treatment, customers picked at random. The gap is the
    value the model adds through selection.
- **Uncertainty.** Each period's estimate has a standard error; a small control group
  dominates it. For a year-to-date total, the incremental counts add and so do their
  variances (independent periods), so the total's interval is tighter than any month's.
- **Months with no significant uplift.** Expected with small controls. Report them as
  they are; do not drop them from the range.
- **Projection.** A full-year figure from part of a year is an extrapolation: state the
  method (run rate, seasonality) and give a range.
- **Revenue proxy.** List price is not billed revenue; discounts, proration and churn
  after upgrade all reduce it. Name the proxy.
- **Checks before trusting a number.** Groups drawn from the same population and date,
  no customer in both groups, same conversion window, same eligibility rules.

## On my CV

"Built uplift tracking and a consolidated revenue table; the outbound model showed +53% to
+77% conversion uplift in most months." Say precisely: this is the model's uplift over
random targeting, measured by me; the model itself was inherited. "Most months" means some
months showed no significant uplift, and I can say why. No absolute counts or revenue in
an interview.

## Likely questions

1. **+60% uplift of what?** Relative conversion rate of model-targeted over
   random-targeted customers in the same campaign and period.
2. **Why were some months not significant?** Control group size and the base rate that
   month; the interval included zero. The estimate was not zero, the evidence was weak.
3. **How do you measure revenue uplift?** Mean revenue per assigned customer in each
   group over a fixed window, difference with a bootstrap interval, proxy stated.
4. **How long after the offer do you count?** A fixed window agreed in advance, long
   enough for the billing cycle; also check whether the uplift persists or is pulled
   forward from later months.
5. **Senior follow-up: finance says the incremental revenue is too small to matter.**
   Compare with the cost of the campaign and the model, show the interval, and separate
   "the model adds over random" from "the campaign is worth running".

## Pitfalls

- Uplift measured on converters only (selection on the outcome).
- Comparing targeted customers with the untargeted rest instead of a random control.
- Presenting a model's measured uplift as uplift I personally caused.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*: <https://experimentguide.com/>
- Zyabkina, "Measuring Incrementality with Universal (Global) Control Groups": <https://zyabkina.com/universal-control-groups-and-advanced-experiments-in-marketing/>
- Bluecore Engineering, "Using Holdout Groups to Quantify Marketing Campaign Lift": <https://medium.com/bluecore-engineering/using-holdout-groups-to-quantify-marketing-campaign-lift-87e6883e3eab>
