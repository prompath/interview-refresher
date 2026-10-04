[Contents](../index.md) · J2 · P1

# Machine learning system design

## In one minute

The system design interview gives an open prompt ("design a next-best-offer system") and
45 minutes. The interviewer watches how I structure it. I follow a fixed order: clarify
requirements, frame the problem and metrics, data and labels, features, model, serving,
evaluation, monitoring. I state trade-offs at each step and start simple.

## Key ideas

- **Framework.**
  1. *Requirements*: users, scale, latency (batch or real time), constraints.
  2. *Framing*: target, online and offline metrics, baseline.
  3. *Data*: sources, labels, delay in labels, biases, privacy.
  4. *Features*: point-in-time correct; batch versus real-time features.
  5. *Model*: simple baseline first, then the main candidate; why.
  6. *Training*: splits by time, retraining cadence.
  7. *Serving*: batch scoring to a table, or an online service; fallbacks.
  8. *Evaluation*: offline, then A/B test with a holdout.
  9. *Monitoring and iteration*: data quality, drift, business metric, feedback loop.
- **Batch versus real time.** Monthly or daily campaigns need batch scoring; an offer
  shown in an app at login needs online serving and precomputed features. Do not design
  real time where batch will do.
- **Multi-stage recommenders.** Candidate generation → ranking → business rules and
  re-ranking.
- **Feedback loops.** The model's own choices shape its future training data. Keep a
  random exploration slice.
- **Worked case: next-best-offer in telecom.**
  - Requirement: one offer per customer per channel per cycle; contact policy; capacity
    of the call centre.
  - Framing: maximise incremental revenue, measured against control groups.
  - Data: profile, usage, billing, past offers and responses.
  - Model: propensity per offer or a recommender, with eligibility rules; later a bandit.
  - Serving: daily batch to a campaign table.
  - Evaluation: global and campaign control groups; uplift over random targeting.
  - Monitoring: score drift, offer mix, conversion by decile.
- **Other cases to rehearse.** Churn prevention (prediction versus uplift, intervention
  cost); demand or load forecast (hierarchy, horizons, retraining); fraud or anomaly
  detection (imbalance, delayed labels); a retrieval-based assistant.
- **What scores well.** Clarifying questions, explicit assumptions, trade-offs, attention
  to measurement and failure modes.

## My evidence

The AIS upsell stack is a real instance of the worked case: propensity models,
recommender plus rules, a bandit, control groups and uplift tracking. I can design from
experience; I should present it generically.

## Likely questions

1. **Design a next-best-offer system.** Use the framework; draw the pipeline.
2. **How would you know it works?** Randomised control and uplift, not offline accuracy.
3. **What breaks first in production?** Upstream data changes and silent rule
   divergence.
4. **How do you handle a new offer with no history?** Rules or exploration, then learn.
5. **Lead-level follow-up: what would you build in the first month with two people?** The
   measurement and a simple baseline, before any complex model.

## Pitfalls

- Jumping to the model.
- No measurement plan.

## Sources

- Huyen, *Designing Machine Learning Systems* (2022): <https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/>
- Huyen, "Machine Learning Systems Design" (interview-oriented notes): <https://huyenchip.com/machine-learning-systems-design/toc.html>
- Google, Recommendation Systems course (multi-stage architecture): <https://developers.google.com/machine-learning/recommendation>
