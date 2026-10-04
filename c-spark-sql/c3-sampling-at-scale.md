[Contents](../index.md) · C3 · P1

# Sampling at scale

## In one minute

Assigning customers to control groups and test buckets in a daily job has to be random,
reproducible and stable: a customer keeps their group, a re-run changes nothing, and new
customers are added by the same rule. I get that from a deterministic hash of a stable
customer key, or from seeded sampling of only the new customers with assignments persisted,
followed by checks on the resulting proportions.

## Key ideas

- **Hash-based assignment.**

  ```
  bucket = hash(customer_key + salt) mod 100
  ```

  Deterministic, needs no stored state, and independent between experiments when each
  uses its own salt. Ranges of the 0-99 value give groups of chosen sizes.
- **Persisted assignment.** Sample once, store the result, and on later days sample only
  customers not yet assigned. Needed when group sizes must be exact or when assignment
  depends on attributes as of the first day.
- **Why not `rand()` or `sample()` alone.** The result depends on partitioning and on
  recomputation; without a seed and a stable input order it is not reproducible. Even
  with a seed, a changed upstream plan can change the outcome.
- **Stratification.** Sample within strata (product line, value tier) so each group
  mirrors the base: `sampleBy` with per-stratum fractions, or a hash within each stratum.
- **Mutual exclusivity.** Draw groups in a fixed order from the remaining pool, or carve
  disjoint ranges of one hash, so no customer sits in two groups that must not overlap.
- **Stable key.** Hash an identifier that survives number or plan changes; decide what
  happens when one person holds several subscriptions.
- **Idempotent writes.** Overwrite the day's partition; a same-day re-run must not append
  duplicates or reassign anyone.
- **Deduplicate before sampling.** Duplicate keys give a customer more than one draw.
- **Checks after sampling.** Proportions against the design (chi-square, as for sample
  ratio mismatch), balance on pre-period metrics, no overlaps, no duplicates. A check
  that only displays a result and does not fail the job is not a check.
- **Guard the evidence.** Tables that record assignments are the experiment's evidence;
  protect them from accidental overwrite.

## On my CV

"Built a daily PySpark job, reusing the holdout's sampling design, that assigns customers
to test buckets for a second vendor's uplift tests." I consolidated ad-hoc notebooks into
one job with shared modules, development and production environments and a write guard,
and fixed defects found on the way (a partition filter applied to the wrong product line,
a duplicate check that reported without deduplicating, failed same-day re-runs).

## Likely questions

1. **How do you make assignment reproducible?** Hash of a stable key with a salt, or
   persisted assignments with only new customers sampled.
2. **Two experiments on the same base: how do you keep them independent?** Different
   salts, so bucket membership in one says nothing about the other.
3. **How do new customers enter?** Assigned on first appearance by the same rule; existing
   assignments never change.
4. **How do you verify the split?** Proportion test against the design and pre-period
   balance, failing the job on violation.
5. **Senior follow-up: someone asks to "top up" a group that shrank through churn.**
   Topping up with fresh customers changes the group's composition; better to analyse the
   original cohort or start a new cohort with its own start date.

## Pitfalls

- Re-sampling everyone each day.
- Hashing a key that changes.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments* (randomisation, bucketing): <https://experimentguide.com/>
- PySpark `DataFrame.sampleBy`: <https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.DataFrame.sampleBy.html>
- PySpark `xxhash64`: <https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.functions.xxhash64.html>
