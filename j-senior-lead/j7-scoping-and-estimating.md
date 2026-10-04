[Contents](../index.md) · J7 · P2

# Scoping and estimating

## In one minute

Data science work is uncertain because the result is unknown until tried. I manage that by
splitting work into short phases with a decision at the end of each (is the data good
enough, does a baseline beat today's process, is the gain worth productionising), by
estimating in ranges, and by agreeing up front what "done" means.

## Key ideas

- **Phases with gates.**
  1. *Discovery*: problem, decision, data availability. Output: one-page scope.
  2. *Feasibility or proof of concept*: baseline on real data. Output: go or no-go.
  3. *Pilot*: limited live test with measurement.
  4. *Production*: pipeline, monitoring, handover.
  Each gate can stop the project cheaply.
- **Proof of concept versus production.** A proof of concept answers "can it work?" on a
  sample with shortcuts. Production adds data pipelines, edge cases, tests, monitoring,
  security and support; usually several times the effort.
- **Time-boxing.** Fix the time, let the scope vary: "two weeks to find out whether the
  data support this".
- **Estimating.** Break into tasks; give a range with stated assumptions; list the
  unknowns that would move it; revise as they resolve. Data access and data quality are
  the usual underestimates.
- **Definition of done.** Not "model trained" but, for example, "scores delivered daily
  to the campaign table, validated, with uplift measured against control and a runbook".
- **Success criteria agreed first.** Metric and threshold, and what happens if missed.
- **Risk register.** Data, technical, adoption, dependency on other teams; each with a
  mitigation or an early test.
- **Scope control.** New requests are welcome and go through the same trade-off: what
  moves out or how the date moves.
- **Presale scoping.** Understand the client's decision and data before promising;
  propose a small paid first phase; state assumptions and exclusions in writing.
- **Build, buy or neither.** Sometimes the right scope is a rule, a dashboard or a
  vendor product.
- **Handover.** Documentation, training, ownership after delivery, planned from the
  start.

## My evidence

"Scoped and built" the gas optimizer and presale proofs of concept at Sertis; the idea
pipeline at AIS (research, plan, pitch); the AutoML product as a lesson in validating
demand before building.

## Likely questions

1. **How do you estimate a project you have never done?** Phases, ranges, named unknowns,
   an early feasibility gate.
2. **How do you prevent a proof of concept from being mistaken for a product?** Say what
   was skipped and what production requires, in the readout.
3. **The data turn out worse than expected halfway.** Raise it at once with options:
   narrower scope, a data fix first, or stop.
4. **What does done mean for a model?** In use, measured, monitored, owned.
5. **Lead-level follow-up: how do you plan a quarter for a team?** Committed items with
   gates, a reserve for maintenance and unplanned requests, and exploration time-boxed.

## Pitfalls

- Single-number estimates.
- No stop criteria.

## Sources

- CRISP-DM process model: <https://en.wikipedia.org/wiki/Cross-industry_standard_process_for_data_mining>
- Zinkevich, "Rules of Machine Learning" (start simple, launch and iterate): <https://developers.google.com/machine-learning/guides/rules-of-ml>
- Huyen, *Designing Machine Learning Systems* (2022): <https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/>
