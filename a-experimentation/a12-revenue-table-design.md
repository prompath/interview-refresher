[Contents](../index.md) · A12 · P2

# Revenue table design

## In one minute

A consolidated revenue table gives every uplift report one agreed source: one row per
customer per period, with the customer's group assignment as of that period and their
revenue under one definition. Its value is consistency. Before it, each analysis rebuilt
revenue its own way and the numbers did not match.

## Key ideas

- **Grain.** State it in one sentence, for example "one row per customer per billing
  month". Every join must preserve it; test for duplicates on the key.
- **Fact and dimensions.** Revenue is the fact; customer, product, campaign and group are
  dimensions. Keep assignment as of the time (a snapshot), not the current value, so
  history is not rewritten when a customer changes group or plan.
- **Slowly changing attributes.** Plan, segment and group change. Either store validity
  ranges (type 2) or snapshot them per period.
- **One revenue definition.** Billed versus list price, before or after discounts, with or
  without tax, recurring versus one-off. Pick one, document it, and name any proxy.
- **Incremental loads.** Partition by period; overwrite a partition on re-run so the job
  is idempotent; late-arriving billing data means recent partitions get reprocessed.
- **Quality checks.** Row count against the customer base, uniqueness of the key, null
  rates, revenue total reconciled with a finance figure, no customer in two groups.
- **Alignment.** Period boundaries of revenue and of group assignment must match (billing
  cycle versus calendar month is a common mismatch).
- **Design for the question.** Columns for pre-period revenue make
  difference-in-differences and CUPED a simple query.

## On my CV

"Built uplift tracking and a consolidated revenue table." No internal table names and no
revenue figures in an interview.

**To fill in (only I know):**

- What was inconsistent before, and who was affected?
- The grain and the revenue definition chosen, and why.
- Which sources were combined (in generic terms: billing, package changes, assignments).
- The checks that run on it and who uses it now.

## Likely questions

1. **What is the grain and how do you enforce it?** State it; a uniqueness test on the key
   in the pipeline.
2. **How do you handle a customer who changes plan mid-month?** By the chosen rule
   (prorated billed amount, or plan at period end), applied the same way to every group.
3. **How do you know the table is right?** Reconciliation against an independent total and
   automated checks on each load.
4. **How do late data affect reports?** Recent periods are provisional; reprocess a
   trailing window and mark reports accordingly.
5. **Senior follow-up: how did you get others to adopt it?** Showed two reports
   disagreeing, agreed the definition with the business owners, and moved the standard
   reports onto it first.

## Pitfalls

- Joins that fan out rows and inflate revenue.
- Using the current group assignment for past periods.

## Sources

- Kimball Group, dimensional modelling techniques (grain, slowly changing dimensions): <https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/dimensional-modeling-techniques/>
- Slowly changing dimension: <https://en.wikipedia.org/wiki/Slowly_changing_dimension>
