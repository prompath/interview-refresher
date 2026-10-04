[Contents](../index.md) · E3 · P3

# Attrition analysis

## In one minute

A predictive attrition model says who is likely to leave; a causal analysis asks what
would make them stay. The two can disagree: a strong predictor (recently updated profile)
may be a symptom, not a lever. The proof of concept used causal discovery to propose which
factors drive attrition, so that the client could choose interventions rather than only
rank people by risk.

## Key ideas

- **Prediction.** Binary classifier or survival model on tenure, pay, role, manager,
  workload, engagement. Output: risk score. Use: prioritise attention.
- **Survival analysis (by name).** Models time until leaving and handles people who have
  not left yet (censoring): Kaplan-Meier curves, Cox proportional hazards.
- **Causal framing.** For each candidate lever (pay rise, promotion, transfer), what is
  the effect on leaving? Needs confounders (performance, market demand for the role)
  handled.
- **Typical traps.**
  - *Reverse causality*: low engagement may follow a decision to leave.
  - *Confounding*: high performers get both promotions and outside offers.
  - *Selection*: data only on those who stayed long enough to be measured.
  - *Leakage*: features recorded during the notice period.
- **Workflow of a causal proof of concept.**
  1. Agree the outcome and the candidate levers.
  2. Encode background knowledge (time order, impossible edges).
  3. Run discovery; check stability.
  4. Review the graph with the client's experts.
  5. Estimate effects for the levers that survive, with adjustment sets from the graph.
  6. Recommend interventions to pilot, ideally as experiments.
- **Ethics.** Individual risk scores for employees are sensitive; prefer group-level
  findings and be explicit about use.

## On my CV

"Built presale proofs of concept ... for causal attrition analysis" (Sertis). Presale: the
aim was to show a prospective client what the approach could tell them.

**To fill in (only I know):**

- Employee or customer attrition, and what data was used (client sample or public data).
- Which algorithm and test in causal-learn, and what background knowledge was encoded.
- What the graph suggested, and how it was presented.
- Whether the proof of concept led to a project.

## Likely questions

1. **Why causal rather than predictive?** The client wanted to know what to change, not
   only whom to watch.
2. **How did you validate the findings?** Stability checks, expert review, and
   consistency with a predictive model; no experiment was possible in a proof of concept.
3. **What were the limitations?** Observational data, possible hidden confounders, small
   sample.
4. **Senior follow-up: how do you sell an uncertain method honestly?** Present it as a
   way to generate and rank hypotheses, state what would confirm them, and propose a
   pilot.

## Pitfalls

- Overstating a proof of concept as a delivered solution.

## Sources

- causal-learn documentation: <https://causal-learn.readthedocs.io/en/latest/>
- lifelines, introduction to survival analysis: <https://lifelines.readthedocs.io/en/latest/Survival%20Analysis%20intro.html>
- Facure, *Causal Inference for the Brave and True*: <https://matheusfacure.github.io/python-causality-handbook/landing-page.html>
