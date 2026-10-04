[Contents](../index.md) · C1 · P1

# Spark execution model

## In one minute

Spark splits data into partitions spread over executor machines and runs the same code on
each partition in parallel. Transformations are lazy: they build a plan. Only an action
(write, count, collect) makes Spark optimise the plan and run it. The driver coordinates;
the executors hold the data. Most performance problems are shuffles (moving data between
partitions) or pulling data to the driver.

## Key ideas

- **Driver and executors.** The driver runs my program, builds the plan and schedules
  tasks. Executors run tasks and store partitions. The driver has limited memory.
- **Lazy evaluation.** `select`, `filter`, `join`, `groupBy` return a new DataFrame and do
  nothing yet. `count`, `collect`, `show`, `write` trigger a job.
- **Job → stages → tasks.** A job is split into stages at shuffle boundaries; each stage
  runs one task per partition.
- **Narrow and wide transformations.** Narrow (filter, select, map): each output partition
  depends on one input partition. Wide (join, groupBy, distinct, orderBy, repartition):
  rows must be redistributed by key, which is a shuffle.
- **Catalyst and Tungsten.** The optimiser rewrites the logical plan (predicate pushdown,
  column pruning, join reordering) into a physical plan; `df.explain()` shows it.
- **Adaptive query execution.** At run time Spark re-plans from actual sizes: coalesces
  small shuffle partitions, switches to broadcast joins, splits skewed partitions.
- **Why `toPandas()` and `collect()` are dangerous.** They pull every row to the driver;
  fine for a small result, fatal for a table. Write with Spark instead.
- **Recomputation.** Without caching, each action recomputes the DataFrame from source.
  This also means a non-deterministic step (random sampling, `row_number` over ties) can
  give different results in two actions on the "same" DataFrame.
- **DataFrame over RDD.** DataFrames go through the optimiser; raw RDD code does not.

## On my CV

"Built a daily PySpark job ... that assigns customers to test buckets." Real examples from
that work: an export built on the driver via pandas that had to be rewritten to a Spark
write, and deduplication that was non-deterministic.

## Likely questions

1. **What happens when you call `df.filter(...).groupBy(...).count()`?** Nothing until an
   action. Then a plan with a filter pushed to the source, a partial aggregation, a
   shuffle by key, and a final aggregation.
2. **Transformation versus action?** A transformation defines a new dataset lazily; an
   action runs the plan and returns or writes a result.
3. **What is a shuffle and why is it expensive?** Redistribution of rows across partitions
   by key: serialisation, network and disk.
4. **Why did the same DataFrame give different counts twice?** It was recomputed and
   contained a non-deterministic step; persist it or make the step deterministic.
5. **Senior follow-up: how do you investigate a slow job?** The Spark UI: which stage is
   slow, shuffle sizes, task time skew, spill; then the physical plan.

## Pitfalls

- Looping over rows on the driver.
- Calling several actions on an uncached, expensive DataFrame.

## Sources

- Spark, cluster mode overview: <https://spark.apache.org/docs/latest/cluster-overview.html>
- Spark, RDD programming guide (transformations, actions, shuffles): <https://spark.apache.org/docs/latest/rdd-programming-guide.html>
- Spark SQL performance tuning (adaptive query execution): <https://spark.apache.org/docs/latest/sql-performance-tuning.html>
