[Contents](../index.md) · K5 · Manager extras

# Measuring the team's value

## In one minute

The value of a data science team is the incremental business result of the decisions its
work changed, less what the team costs. I would report it from controlled measurement
wherever possible: holdouts and experiments give a defensible number, and I would rather
present a smaller figure with a method behind it than a large one built on attribution.

## Key ideas

- **Incremental, not total.** Revenue from customers the model targeted is not the
  model's value. The value is the difference from what would have happened: against a
  control group, random targeting or the previous process.
- **Measurement built in.** Every deployed model has a comparison group and a tracked
  outcome from day one. This is the strongest position a data science manager can hold.
- **Return on investment.**

  ```
  ROI = (incremental value − cost) / cost
  cost = people + platform and compute + vendor fees + cost of the action (calls, discounts)
  ```

- **Kinds of value.**
  - *Revenue uplift* (upsell, pricing).
  - *Cost saved* (optimisation, automation, fewer wasted contacts).
  - *Risk reduced* (churn, fraud).
  - *Decision quality and speed* (harder to price; use adoption and time saved).
- **Avoid double counting.** Several teams claim the same revenue. A global holdout gives
  one total to share out.
- **Leading and lagging indicators.** Models in production, tests run, adoption by the
  business (leading); incremental revenue or cost (lagging).
- **Team health metrics.** Time from idea to production, share of time on maintenance,
  incidents, share of projects reaching production.
- **Reporting to executives.** One page: outcome in money with a range, how it was
  measured in one sentence, what is next, what is needed. No model metrics.
- **Reporting nulls.** A stopped project that saved further spend is value; say so.
- **Credibility.** Agree the measurement method with finance before the results exist.
- **The honest caveat.** Some work (foundations, data quality, enabling others) has
  indirect value; describe it by what it made possible.

## My evidence

This is my strongest link to management: I built uplift tracking and a consolidated
revenue table, and measured a model's uplift against random targeting with intervals.
Percentages only in interviews; no absolute figures.

## Likely questions

1. **How would you show the value of your team?** Incremental results from control
   groups, costs included.
2. **Finance does not believe the numbers. What do you do?** Walk through the method,
   agree definitions with them, use their revenue figures.
3. **What metrics would you report monthly?** Incremental outcome, adoption, health.
4. **How do you value a project with no direct revenue?** Time saved, risk avoided, or
   what it enabled; stated as such.
5. **The measured uplift is small. Do you report it?** Yes, with the interval and a
   recommendation.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments* (holdouts and organisational metrics): <https://experimentguide.com/>
- Zyabkina, "Measuring Incrementality with Universal (Global) Control Groups": <https://zyabkina.com/universal-control-groups-and-advanced-experiments-in-marketing/>
