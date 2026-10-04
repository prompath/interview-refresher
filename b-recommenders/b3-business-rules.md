[Contents](../index.md) · B3 · P1

# Business rules on top of a model

## In one minute

A production recommender is a model plus rules. The model ranks; the rules decide what is
allowed (eligibility, contracts, price steps), what must be shown, and what to fall back
to when the model has nothing good. Most production bugs and most stakeholder questions
are in the rules, so I keep them as explicit, tested configuration rather than code
scattered through the pipeline.

## Key ideas

- **Where rules sit.**
  - *Pre-filter*: remove ineligible candidates before scoring.
  - *Post-filter*: remove or replace items after scoring.
  - *Re-rank*: adjust order for margin, strategy or diversity.
  - *Fallback or override*: a default when confidence is low or no candidate survives.
- **Typical rule types.** Eligibility (plan, device, contract), exclusions (already holds
  it, incompatible promotion), price or step limits (do not offer more than a set step
  above current spend), must-include offers, frequency caps.
- **Gating by another model.** A rule can depend on a score, for example replacing the
  top offer with a conservative mapped offer when purchase propensity is low.
- **Rules as data.** Mapping tables and thresholds in config, with version history, so a
  change is a reviewed diff, not a code edit.
- **Testing rules.** Unit tests per rule with boundary cases (is the threshold `>` or
  `>=`?), plus an end-to-end check that every customer gets a valid offer.
- **Any versus all.** Exclusion logic is a common bug: "allowed if any promotion permits
  it" is different from "blocked if any promotion forbids it".
- **Audit against the rulebook.** Compare the code rule by rule with the business's
  document; list divergences; agree which side is right before changing anything.
- **Measure the rules.** How many recommendations each rule changes, and the conversion
  of rule-driven versus model-driven offers. Rules can erase the model's value.
- **Explaining a case.** Trace one customer through each step to answer "why did this
  customer get this offer?"

## On my CV

"Adjusted and extended the package recommender and its business rules with the business
team, and made it production-ready." Examples I can describe in generic terms: a
propensity-gated override for low-propensity customers; mapping-based offers; an audit of
the code against the business rulebook that found divergences; tracing the business
team's feedback cases to their cause in the code. No internal names.

## Likely questions

1. **Why not let the model learn the rules?** Rules encode constraints the data cannot
   show (contracts, strategy, regulation) and must hold every time.
2. **How do you keep code and rulebook in sync?** One source for thresholds and mappings,
   tests on boundaries, and a periodic audit.
3. **The business reports a wrong recommendation. What do you do?** Reproduce for that
   customer, trace step by step, classify as data, rule or model, and report back.
4. **A new rule is requested for next week.** Estimate how many customers it affects and
   what it does to expected conversion before agreeing.
5. **Senior follow-up: rules keep piling up.** Measure each rule's impact, retire those
   with none, and test contested rules in an experiment.

## Pitfalls

- Thresholds hard-coded in several places.
- Evaluating the model before rules and reporting it as the system's performance.

## Sources

- Google, Recommendation Systems course (candidate generation, scoring, re-ranking): <https://developers.google.com/machine-learning/recommendation>
- Zinkevich, "Rules of Machine Learning" (heuristics and when to keep them): <https://developers.google.com/machine-learning/guides/rules-of-ml>
