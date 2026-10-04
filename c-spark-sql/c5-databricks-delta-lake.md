[Contents](../index.md) · C5 · P2

# Databricks and Delta Lake

## In one minute

Databricks is a managed Spark platform: notebooks, clusters, scheduled jobs and a table
catalogue. Delta Lake is its table format: Parquet files plus a transaction log, which adds
atomic writes, updates and merges, schema enforcement and the ability to query earlier
versions. For a daily pipeline that means safe re-runs and a way back after a bad write.

## Key ideas

- **Delta transaction log.** Each write is a commit listing files added and removed.
  Readers see a consistent snapshot; a failed write leaves no partial data (ACID).
- **Write modes.** `append`; `overwrite` (whole table); partition overwrite with
  `replaceWhere` or dynamic partition overwrite, which is what makes a daily job
  idempotent.
- **`MERGE INTO`.** Upsert: update matching rows, insert new ones. Used for persisted
  assignments and slowly changing data.
- **Time travel.** `VERSION AS OF` or `TIMESTAMP AS OF` to read an old version; `RESTORE`
  to roll back. History is kept until `VACUUM` removes old files.
- **Schema enforcement and evolution.** Writes with a mismatched schema fail unless
  evolution is enabled deliberately.
- **Layout.** Partition by a low-cardinality column that queries filter on (date).
  `OPTIMIZE` compacts small files; Z-ordering or liquid clustering co-locates rows by
  other columns.
- **Medallion layers.** Bronze (raw), silver (cleaned, conformed), gold (business-level
  tables such as a consolidated revenue table).
- **Jobs and workflows.** Tasks with dependencies, schedules, retries, parameters and job
  clusters (started for the run, cheaper than all-purpose clusters).
- **Notebooks versus code.** Repos with modules imported by thin notebooks or Python
  tasks; parameters through widgets or job parameters; separate development and
  production targets.
- **Unity Catalog.** Central governance: three-level names (`catalog.schema.table`),
  permissions and lineage.
- **MLflow.** Tracking of runs, parameters, metrics and models; model registry.

## On my CV

Databricks is in Platforms and Tools; the bucket assignment job and the model pipelines
run there. I defined the job for the sampling pipeline with development and production
environments and a write guard on evidence tables.

## Likely questions

1. **Why Delta rather than plain Parquet?** Atomic writes, merges, schema enforcement and
   time travel.
2. **How do you make a daily job safe to re-run?** Overwrite exactly that day's partition,
   or merge on the key.
3. **A bad run corrupted yesterday's table. What now?** Check the table history, restore
   the previous version, fix and re-run.
4. **How do you structure code on Databricks?** Modules in a repo, tests runnable outside
   the notebook, a job definition under version control.
5. **Senior follow-up: how do you separate development from production?** Separate
   catalogues or schemas selected by config, restricted write permission on production,
   deployment from the main branch only.

## Pitfalls

- Overwriting a whole table when one partition was meant.
- Relying on time travel after `VACUUM`.

## Sources

- Delta Lake documentation: <https://docs.delta.io/latest/index.html>
- Databricks, "What is the medallion lakehouse architecture?": <https://docs.databricks.com/aws/en/lakehouse/medallion>
- Databricks, Lakeflow Jobs: <https://docs.databricks.com/aws/en/jobs/>
