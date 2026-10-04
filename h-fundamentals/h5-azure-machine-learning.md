[Contents](../index.md) · H5 · P3

# Azure Machine Learning

## In one minute

Azure Machine Learning is Microsoft's managed service for the machine learning lifecycle:
a workspace that holds data references, compute, experiments, models and endpoints. I hold
the Azure Data Scientist Associate certification (DP-100) and know the concepts; I have
not used Azure in production work, and I say so.

## Key ideas

- **Workspace.** The top-level container; linked to storage, a key vault, a container
  registry and application insights.
- **Compute.**
  - *Compute instance*: a personal development machine.
  - *Compute cluster*: autoscaling nodes for training jobs.
  - *Serverless compute*; *attached compute* (for example Databricks).
- **Data.** Datastores (connections to storage) and data assets (versioned references to
  files, folders or tables).
- **Environments.** Versioned Docker image plus conda or pip dependencies.
- **Jobs.** A command job runs a script on compute with an environment; a sweep job tunes
  hyperparameters; a pipeline job chains components with defined inputs and outputs.
- **Tracking.** MLflow is the tracking API: parameters, metrics, artefacts, models.
- **Model registry.** Versioned models, registered from job outputs.
- **Deployment.**
  - *Managed online endpoint*: real-time scoring, with traffic split between deployments
    (blue-green).
  - *Batch endpoint*: scoring large data on a cluster.
- **Automated machine learning.** Tries algorithms and preprocessing for classification,
  regression and forecasting.
- **Designer.** Drag-and-drop pipelines.
- **Responsible AI.** Dashboard for interpretability, error analysis and fairness.
- **Interfaces.** Studio (web), Python SDK v2 (`azure-ai-ml`), CLI v2 with YAML
  definitions.
- **Mapping to what I use.** Databricks jobs ↔ Azure ML jobs and pipelines; MLflow is
  common to both; Delta tables ↔ data assets.

## On my CV

"Microsoft Certified: Azure Data Scientist Associate" (June 2025). No cloud platform in
Skills, deliberately: certification only.

## Likely questions

1. **Have you used Azure ML in production?** No. I hold the certification and work on
   Databricks, where the concepts carry over.
2. **How would you deploy a model for real-time scoring?** Register the model, define the
   environment and scoring script, create a managed online endpoint and deployment, test,
   then shift traffic.
3. **Online versus batch endpoint?** Low-latency per request versus scheduled scoring of
   many rows; campaign scoring is batch.
4. **Why did you take the certification?** My real reason, in a sentence (only I know).
5. **Senior follow-up: how would you choose between Azure ML and Databricks?** By where
   the data and the team's skills already are; both cover tracking, jobs and serving.

## Pitfalls

- Implying hands-on experience.

## Sources

- Microsoft Learn, Azure Machine Learning documentation: <https://learn.microsoft.com/en-us/azure/machine-learning/>
- Microsoft Learn, Azure Data Scientist Associate certification: <https://learn.microsoft.com/en-us/credentials/certifications/azure-data-scientist/>
- MLflow documentation: <https://mlflow.org/docs/latest/index.html>
