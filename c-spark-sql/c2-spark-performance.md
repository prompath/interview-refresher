[Contents](../index.md) · C2 · P1

# Spark performance

## In one minute

I make a Spark job faster by reading less (filter on partition columns, select only needed
columns), shuffling less (broadcast small tables, avoid needless wide operations),
handling skewed keys, using built-in functions instead of Python UDFs, and caching only
what is reused. I check the plan and the Spark UI rather than guessing.

## Key ideas

- **Read less.** Partition pruning: filter on the partition column so whole folders are
  skipped. Column pruning and predicate pushdown work with Parquet and Delta.
- **Join strategies.**
  - *Broadcast hash join*: a small table is copied to every executor; no shuffle of the
    large side. Triggered automatically under a size threshold or with `broadcast(df)`.
  - *Sort-merge join*: both sides shuffled and sorted by key; the default for two large
    tables.
  - *Shuffle hash join*: shuffle, then hash the smaller side per partition.
- **Skew.** A few keys hold most rows, so a few tasks run far longer. Fixes: adaptive
  skew-join handling, salting the key, handling the heavy keys separately, filtering null
  keys before the join.
- **Partition count.** Too few: huge tasks and spill. Too many: overhead and tiny files.
  `repartition(n, key)` shuffles to n partitions; `coalesce(n)` reduces without a full
  shuffle.
- **UDFs.**
  - *Built-in functions*: run in the JVM, optimised. First choice.
  - *Python UDF*: rows serialised to a Python process one at a time. Slow.
  - *pandas UDF*: batches transferred with Arrow and processed vectorised. Use when
    Python logic is unavoidable (model inference).
- **Caching.** `cache()` or `persist()` when a DataFrame is used several times; unpersist
  after. Caching everything wastes memory.
- **Small files.** Many tiny output files slow later reads; compact or control the number
  of output partitions.
- **Window functions.** A window without `partitionBy` moves everything to one partition.
- **Counting twice.** `df.count()` just to log a number recomputes the pipeline.

## On my CV

PySpark is in Skills and the bucket assignment job. Have one concrete tuning story (what
was slow, how I found it, what changed, the result) in generic terms.

## Likely questions

1. **When does Spark choose a broadcast join?** When one side is estimated under the
   broadcast threshold, or when hinted.
2. **How do you detect and fix skew?** Task duration and shuffle read size uneven in the
   Spark UI; adaptive execution, salting or isolating the hot keys.
3. **`repartition` versus `coalesce`?** Repartition does a full shuffle and can increase
   partitions or partition by key; coalesce merges partitions without a full shuffle.
4. **Why is a Python UDF slow and what replaces it?** Per-row serialisation between JVM
   and Python; built-ins or a pandas UDF.
5. **Senior follow-up: the job is slow and the cluster is expensive. Where first?** The
   data read (pruning), then the largest shuffle, before touching cluster size.

## Pitfalls

- Broadcasting a table that is not small.
- `orderBy` on a whole large table when only a per-group order is needed.

## Sources

- Spark SQL performance tuning (join hints, adaptive execution, skew): <https://spark.apache.org/docs/latest/sql-performance-tuning.html>
- PySpark, pandas UDFs and Arrow: <https://spark.apache.org/docs/latest/api/python/tutorial/sql/arrow_pandas.html>
- Spark tuning guide: <https://spark.apache.org/docs/latest/tuning.html>
