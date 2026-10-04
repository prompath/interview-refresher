[Contents](../index.md) · B7 · P2

# Production readiness

## In one minute

A model is production-ready when someone other than its author can run, change and debug
it safely: configuration is separate from code, logic lives in tested modules rather than
notebook cells, runs are repeatable and safe to re-run, there are separate development and
production environments, and failures and drift are noticed.

## Key ideas

- **Config versus code.** Dates, table locations, thresholds and mappings in config files,
  one per environment. No values edited in notebooks before a run.
- **Modules, not notebooks.** Functions in importable modules with tests; notebooks or job
  entry points only orchestrate.
- **Idempotent runs.** Running the same day twice gives the same result and no duplicates
  (overwrite the partition, deterministic sampling, fixed seeds).
- **Environments.** Development writes to development tables. Production tables that hold
  evidence get a write guard.
- **Data validation.** Checks on inputs (schema, freshness, row counts, nulls) and outputs
  (one row per customer, no ineligible offers, score distribution).
- **Tests.** Unit tests for transformations and rules; a small end-to-end run on sample
  data.
- **Version control and review.** Branches, pull requests, a linter and tests in CI.
- **Scale habits.** No collecting large data to the driver; deduplicate deterministically.
- **Monitoring.** Job success, data volumes, feature and score drift, downstream outcome
  (conversion by decile).
- **Documentation.** How to run, what each step does, known issues.
- **Known technical debt list.** Written down, prioritised, not hidden.

## On my CV

"... made it production-ready" and "Wrote the team's coding standards" (Sertis). At AIS I
moved inherited pipelines to the team's project template: config files, utility modules,
functions decoupled from notebooks. The CI itself was built by a machine learning
engineer; I used it and did not build it.

**To fill in (only I know):** two or three concrete before-and-after examples of what
"production-ready" changed, in generic terms.

## Likely questions

1. **What was not production-ready before?** Give the concrete examples: values edited by
   hand, duplicated logic, a check that was displayed but not enforced.
2. **How do you refactor without changing behaviour?** Run old and new on the same input
   and compare outputs row by row before switching.
3. **Notebook or package?** Notebooks for exploration and thin entry points; logic in
   modules so it can be tested and reviewed.
4. **What do you monitor after deployment?** Run status, input freshness, output
   distributions, and the business outcome.
5. **Senior follow-up: how do you prioritise technical debt against requests?** Tie each
   item to a risk (wrong offers, failed runs, slow changes) and fix what blocks or
   endangers current work first.

## Pitfalls

- Saying "production-ready" without a concrete example.
- Claiming the CI.

## Sources

- Sculley et al., "Hidden Technical Debt in Machine Learning Systems" (2015): <https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems>
- Breck et al., "The ML Test Score" (2017): <https://research.google/pubs/the-ml-test-score-a-rubric-for-ml-production-readiness-and-technical-debt-reduction/>
- Zinkevich, "Rules of Machine Learning": <https://developers.google.com/machine-learning/guides/rules-of-ml>
