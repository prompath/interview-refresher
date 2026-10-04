[Contents](../index.md) · J1 · P1

# Problem framing

## In one minute

Before any modelling I pin down the decision the work will change: who decides what, how
often, and what they do today. From that follow the target, the metric, the baseline to
beat and the simplest thing that could work. A senior data scientist is judged more on
choosing and shaping the right problem than on the model.

## Key ideas

- **Start from the decision.** "Which customers do we call this month, with which offer?"
  is a decision. "Build a churn model" is not.
- **Questions to ask.**
  - What happens today, and what does it cost or lose?
  - What action will be taken on the output, by whom, how often?
  - What would success look like in a number, and by when?
  - What constraints apply (capacity, budget, regulation, contact policy)?
  - What data exist at the moment the decision is made?
- **Translate to a technical problem.** Prediction (who will buy), causal (what will
  change behaviour), optimisation (how to allocate), or description (what happened).
  Mistaking a causal question for a predictive one is the commonest framing error.
- **Target definition.** Precise event, window and population. Small changes in the
  definition change the model more than the algorithm does.
- **Metric chain.** Business outcome (incremental revenue) ← online metric (conversion
  uplift) ← offline metric (lift in top decile). State how each links to the next.
- **Baseline.** Current process, a simple rule, or random. Without it there is no claim.
- **Value estimate.** Size of the population × achievable improvement × value per unit,
  against cost to build and run. A rough number decides whether to start.
- **When not to use a model.** A rule does as well; no action can be taken on the
  prediction; data at decision time are missing; the cost of errors is too high to
  automate.
- **Smallest useful version.** A heuristic or simple model with measurement in place,
  then iterate.
- **Risks named up front.** Data access, label quality, adoption, measurement.
- **Written one-pager.** Problem, decision, metric, baseline, approach, risks,
  milestones; agreed with the stakeholder before work starts.

## My evidence

Presale scoping at Sertis (the optimizer was "scoped and built"); at AIS, working with the
business team on what the recommender's rules should achieve; measurement work that
separated "does the campaign work" from "does the model add value".

## Likely questions

1. **A stakeholder asks for a churn model. What do you do first?** Ask what they will do
   with the scores and whether the intervention works; that may make it an uplift or
   experiment question.
2. **How do you decide a project is worth doing?** Rough value estimate against effort,
   and whether the result can be measured.
3. **Tell me about a time the original ask was the wrong problem.** A prepared story.
4. **How do you choose the metric?** Work back from the business outcome and check the
   proxy moves with it.
5. **Lead-level follow-up: how do you teach framing to juniors?** Have them write the
   one-pager and defend the baseline before any code.

## Pitfalls

- Accepting the requested solution as the problem.
- No baseline.

## Sources

- Zinkevich, "Rules of Machine Learning": <https://developers.google.com/machine-learning/guides/rules-of-ml>
- Google, "Introduction to Machine Learning Problem Framing": <https://developers.google.com/machine-learning/problem-framing>
- Huyen, *Designing Machine Learning Systems* (2022): <https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/>
