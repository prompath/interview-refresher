[Contents](../index.md) · C4 · P1

# SQL

## In one minute

For a senior role SQL questions test whether I state the grain of each table, join without
multiplying rows, and reach for window functions for "latest per customer", running totals
and period-over-period comparisons. I say the grain out loud before writing the query.

## Key ideas

- **Logical order.** `FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT (windows) → ORDER
  BY → LIMIT`. This is why a window result cannot be filtered in `WHERE`; wrap it in a
  CTE or use `QUALIFY` where supported.
- **Joins.** Inner, left, full, cross, semi (`EXISTS`), anti (`NOT EXISTS`). A join on a
  non-unique key multiplies rows. A filter on the right table in `WHERE` turns a left
  join into an inner join; put it in `ON`.
- **Nulls.** `NULL = NULL` is not true; `NOT IN` with a null in the list returns nothing;
  `COUNT(col)` skips nulls, `COUNT(*)` does not.
- **Window functions.**

  ```sql
  ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY event_date DESC)   -- latest row
  SUM(amount)  OVER (PARTITION BY customer_id ORDER BY month)             -- running total
  LAG(amount)  OVER (PARTITION BY customer_id ORDER BY month)             -- previous period
  ```

  `ROW_NUMBER` is unique, `RANK` leaves gaps on ties, `DENSE_RANK` does not. Frames:
  `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW` for a moving average.
- **Deduplication.** `ROW_NUMBER() ... = 1` with a tie-breaker that makes the order total;
  otherwise the result is non-deterministic.
- **Conditional aggregation.** `SUM(CASE WHEN grp = 'treatment' THEN converted END)` to
  pivot groups into columns.
- **CTEs.** Name each step; one grain per CTE.
- **Standard patterns.** Conversion rate by group; cohort retention (first-event month
  joined to later activity); funnel (ordered steps per customer); gaps and islands
  (consecutive periods); top n per group.
- **Performance.** Filter on partition columns early; avoid `SELECT *`; avoid functions on
  join keys; check the plan.

## On my CV

SQL is in Skills and behind the uplift tracking and revenue table. Practise aloud:
"conversion rate and uplift by month and group from an assignment table and a transaction
table", including the pitfall of customers with several transactions.

## Likely questions

1. **Latest plan per customer?** `ROW_NUMBER()` partitioned by customer ordered by date
   descending with a tie-breaker, keep 1.
2. **`WHERE` versus `HAVING`?** `WHERE` filters rows before grouping, `HAVING` filters
   groups after.
3. **Why did my join double the revenue?** The other side was not unique on the key;
   aggregate it to the join grain first.
4. **Month-over-month change per customer?** `LAG` over month, then the difference.
5. **Senior follow-up: how do you review a colleague's query?** Check the grain of each
   step, the uniqueness of join keys, null handling and the date boundaries, then
   readability.

## Pitfalls

- `COUNT(DISTINCT ...)` used to hide a fan-out instead of fixing the join.
- Inclusive versus exclusive date boundaries.

## Sources

- Spark SQL window functions: <https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select-window.html>
- PostgreSQL tutorial on window functions: <https://www.postgresql.org/docs/current/tutorial-window.html>
- Mode, SQL tutorial (joins, windows, performance): <https://mode.com/sql-tutorial/>
