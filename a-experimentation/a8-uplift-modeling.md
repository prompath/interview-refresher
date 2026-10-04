[Contents](../index.md) · A8 · P3

# Uplift modeling (awareness)

## In one minute

Uplift *modeling* predicts, per customer, how much a treatment changes their outcome, so
that offers go to those who respond *because* of the offer. I have measured uplift with
experiments but have not built uplift models; the models I work with are propensity
models, which predict who will buy, not who will be persuaded.

## Key ideas

- **Target.** The conditional average treatment effect:
  $$\tau(x) = E[Y \mid X = x, \text{treated}] - E[Y \mid X = x, \text{control}]$$.
- **Four segments.** Persuadables (buy only if treated), sure things (buy anyway), lost
  causes (never buy), sleeping dogs (buy only if left alone). A propensity model ranks
  sure things highest; an uplift model ranks persuadables highest.
- **Needs experimental data.** Training requires both treated and randomly untreated
  customers. The control group from uplift measurement is exactly that data.
- **Meta-learners.**
  - *S-learner*: one model with treatment as a feature; uplift = prediction with
    treatment on minus off. Tends to shrink the effect towards zero.
  - *T-learner*: one model per group; uplift = difference. Noisy when one group is small.
  - *X-learner*: imputes individual effects from the T-learner's models and fits models to
    those; better with unbalanced groups.
- **Direct methods.** Uplift trees and causal forests split to maximise the difference in
  effect between leaves.
- **Evaluation.** No individual ground truth exists, so evaluate by ranking: sort by
  predicted uplift, plot cumulative incremental conversions (Qini or uplift curve), and
  summarise as area under it (AUUC, Qini coefficient).

## On my CV

Skills says "uplift measurement". If asked "have you built an uplift model?": no; I
designed the experiments and measured conversion and ARPU uplift; the data from those
control groups is what an uplift model would train on, and I know the approach.

## Likely questions

1. **Propensity versus uplift model?** Propensity predicts the outcome; uplift predicts
   the change in outcome caused by treatment.
2. **Why can a good propensity model waste budget?** It targets customers who would have
   bought anyway.
3. **How would you evaluate an uplift model?** Qini curve on a held-out randomised set,
   then an A/B test of uplift-targeted against propensity-targeted.
4. **Which learner would you start with?** T-learner as a baseline, X-learner if the
   control group is small relative to treated.
5. **Senior follow-up: would you move the current models to uplift?** Only if the
   random-control data is large enough and an experiment shows better incremental revenue
   than propensity targeting; uplift models are noisier and harder to maintain.

## Pitfalls

- Saying "uplift modeling" when meaning uplift measurement.
- Evaluating an uplift model with AUC.

## Sources

- Facure, *Causal Inference for the Brave and True*, Meta Learners: <https://matheusfacure.github.io/python-causality-handbook/21-Meta-Learners.html>
- Künzel et al., "Metalearners for estimating heterogeneous treatment effects" (2019): <https://arxiv.org/abs/1706.03461>
- Uplift modelling overview: <https://en.wikipedia.org/wiki/Uplift_modelling>
