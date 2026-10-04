[Contents](../index.md) · E1 · P2

# Causal inference basics

## In one minute

Causal inference asks what would happen if we intervened, not what tends to occur together.
Each unit has two potential outcomes, with and without treatment, and only one is ever
seen. Randomisation makes the groups comparable so the difference in means is the effect.
Without randomisation, I must argue that after adjusting for the right variables the
groups are comparable, and say which assumption carries the argument.

## Key ideas

- **Potential outcomes.** $$Y(1)$$, $$Y(0)$$; the individual effect $$Y(1) - Y(0)$$ is never
  observed.
- **Estimands.**
  - *ATE*: average effect over everyone.
  - *ATT*: average effect on those treated.
  - *CATE*: average effect for a subgroup $$X = x$$.
- **Confounder.** A variable that causes both treatment and outcome. Comparing treated
  and untreated without adjusting mixes its effect in.
- **Causal graph (DAG).** Nodes are variables, arrows are direct causes.
  - *Fork* (`T ← Z → Y`): confounding; adjust for `Z`.
  - *Chain* (`T → M → Y`): mediator; adjusting for `M` blocks part of the effect.
  - *Collider* (`T → C ← Y`): adjusting for `C` *creates* a false association.
- **Backdoor criterion.** Adjust for a set of variables that blocks every path from
  treatment to outcome that starts with an arrow into treatment, without including
  descendants of treatment.
- **Assumptions for observational estimates.** No unmeasured confounding
  (ignorability); overlap (every kind of unit has some chance of each treatment);
  consistency and no interference.
- **Methods.**
  - *Regression adjustment*: include confounders as covariates.
  - *Matching*: compare each treated unit with similar untreated ones.
  - *Propensity score* $$e(x) = P(T = 1 \mid X = x)$$: match or stratify on it, or weight by
    $$1/e$$ and $$1/(1-e)$$ (inverse propensity weighting).
  - *Doubly robust*: combines an outcome model and a propensity model; right if either
    is.
  - *Natural experiments*: difference-in-differences, instrumental variables, regression
    discontinuity.
- **Sensitivity analysis.** How strong would an unmeasured confounder need to be to erase
  the result?

## On my CV

"Built presale proofs of concept ... for causal attrition analysis" (Sertis), and the
reasoning behind all the AIS measurement work. "Propensity score" here is the probability
of *treatment*; at AIS "propensity model" means probability of *purchase*. Do not mix
them.

## Likely questions

1. **Correlation versus causation, with an example?** Customers who get called buy more,
   but they were chosen because they were likely to buy.
2. **What is a confounder and how do you handle it?** Common cause of treatment and
   outcome; randomise, or adjust for it.
3. **Why not control for everything?** Mediators and colliders: adjusting for them biases
   the estimate.
4. **When can you not randomise, and what then?** Ethical, legal or operational limits;
   use a natural experiment or adjustment with stated assumptions.
5. **Senior follow-up: how confident are you in an observational estimate?** Less than in
   an experiment; I give the assumptions, a sensitivity analysis, and propose a test to
   confirm.

## Pitfalls

- Reading a predictive model's feature importance as causal effect.
- Adjusting for variables measured after treatment.

## Sources

- Facure, *Causal Inference for the Brave and True*: <https://matheusfacure.github.io/python-causality-handbook/landing-page.html>
- Cunningham, *Causal Inference: The Mixtape*: <https://mixtape.scunning.com/>
- Hernán and Robins, *Causal Inference: What If*: <https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/>
