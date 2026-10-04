[Contents](../index.md) · J4 · P1

# Model lifecycle and MLOps

## In one minute

A model in production is a pipeline that must keep working as data, code and the world
change. MLOps is the practice that makes this routine: everything versioned, training and
deployment automated and repeatable, the model and its inputs monitored, and a clear way
to retrain or roll back. I have run and maintained such pipelines; the CI was built by an
engineer and I worked within it.

## Key ideas

- **Lifecycle.** Frame → data → train → validate → deploy → monitor → retrain or retire.
- **Version three things.** Code (Git), data (snapshots, Delta versions), model
  (registry with the training run's parameters and metrics).
- **Experiment tracking and registry.** MLflow: runs, parameters, metrics, artefacts;
  registered model versions with stages or aliases.
- **CI/CD for machine learning.** On each change: lint, tests, and for model changes a
  validation step (metric not worse than the current model on a fixed set). Deployment
  from the main branch through development to production.
- **Deployment patterns.** Batch scoring job; online endpoint. *Shadow* (new model scores
  silently), *canary* (small traffic share), *A/B* (randomised comparison), *champion and
  challenger*.
- **Drift.**
  - *Data drift*: input distributions change (population stability index, KS test).
  - *Concept drift*: the relation between inputs and target changes; seen in falling
    performance once labels arrive.
  - *Upstream changes*: a column's meaning or source changes. The most common in
    practice.
- **Monitoring layers.** Job health → data quality (schema, nulls, volumes, freshness) →
  score distribution → performance on matured labels → business outcome.
- **Retraining.** On a schedule, or triggered by drift or performance; always validated
  against the current model before promotion. Delayed labels set the earliest possible
  cadence.
- **Rollback.** Previous model version and previous output table kept and restorable.
- **Feature store (by name).** One definition of each feature for training and serving,
  with point-in-time retrieval; avoids training-serving skew.
- **Maturity levels.** Manual notebooks → automated training pipeline → automated CI/CD
  with monitoring and triggered retraining.
- **Governance.** Ownership, documentation (model cards), access control, audit trail,
  personal data rules.
- **Runbooks.** What to do when the job fails or the output looks wrong, written before
  the incident.

## My evidence

Maintaining production upsell models at AIS; moving pipelines to a project template with
config and modules; development and production environments for the sampling job;
uplift tracking as the business-level monitor.

## Likely questions

1. **How do you know a production model has gone bad?** The monitoring layers, ending
   with the business metric against control.
2. **Data drift versus concept drift?** Inputs change versus the relationship changes.
3. **How often do you retrain?** As often as labels and drift justify; with a gate.
4. **How do you deploy a new model safely?** Shadow or challenger against the champion,
   then promote with rollback available.
5. **Lead-level follow-up: the team has ten models and no monitoring. Where do you
   start?** Inventory with owners, then data-quality checks and outcome tracking on the
   models with the most business exposure.

## Pitfalls

- Claiming to have built CI/CD.
- Monitoring accuracy only, when labels arrive weeks late.

## Sources

- Google Cloud, "MLOps: Continuous delivery and automation pipelines in machine learning": <https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning>
- Sculley et al., "Hidden Technical Debt in Machine Learning Systems" (2015): <https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems>
- MLflow documentation: <https://mlflow.org/docs/latest/index.html>
