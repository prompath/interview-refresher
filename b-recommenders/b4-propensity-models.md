[Contents](../index.md) · B4 · P1

# Propensity models

## In one minute

A propensity model is a binary classifier that scores each customer's probability of an
action (accepting an upsell) so the campaign targets the top of the ranking. Gradient
boosted trees are the standard choice for tabular customer data. I judge it by how well it
ranks (lift in the top deciles) and whether its probabilities are calibrated, and
ultimately by uplift against random targeting.

## Key ideas

- **Gradient boosting.** Trees added one at a time, each fitted to the gradient of the
  loss of the current ensemble. Key controls: learning rate, number of trees, depth,
  subsampling, regularisation; early stopping on a validation set.
- **XGBoost.** Second-order gradients, regularised objective, built-in handling of
  missing values, level-wise trees.
- **CatBoost.** Native categorical features using ordered target statistics (avoids
  target leakage), symmetric trees, good defaults.
- **Class imbalance.** Buyers are rare. Prefer keeping the data as is and using a proper
  metric; class weights if needed. Resampling distorts probabilities, so recalibrate.
- **Metrics.**
  - *ROC AUC*: ranking quality, insensitive to imbalance.
  - *PR AUC*: more informative when positives are rare.
  - *Lift and gain by decile*: conversion in the top 10% divided by the average; what the
    campaign actually uses.
  - *Calibration*: predicted 5% should convert at about 5%; reliability plot, Brier score;
    fix with Platt scaling or isotonic regression.
- **Leakage.** Features that include information from after the scoring date. Build
  features strictly as of a cut-off date; validate on a later period (out-of-time).
- **Label definition.** Who is a positive, over what window, and among whom (only
  customers who were offered?). Training only on contacted customers gives selection
  bias.
- **Tuning.** Optuna: Bayesian (TPE) search with pruning of poor trials. Tune on time-based
  validation.
- **Explanation.** SHAP values: each feature's contribution to a prediction; global
  importance from mean absolute SHAP.
- **Propensity is not uplift.** See [A8](../a-experimentation/a8-uplift-modeling.md).

## On my CV

"Maintained production upsell models: ... propensity models for customer targeting."
Maintained, not built. I refactored one pipeline to the team template without changing
model behaviour, and measured its uplift.

## Likely questions

1. **Why boosting over logistic regression?** Handles non-linearities, interactions and
   missing values with little preparation; logistic regression remains the baseline.
2. **AUC is 0.80. Is the model good?** Not enough to say; show lift in the deciles the
   campaign calls and the uplift over random.
3. **How do you prevent leakage?** Point-in-time features, out-of-time validation, and
   suspicion of any feature with implausibly high importance.
4. **How do you know when to retrain?** Monitor score distribution, feature drift and
   decile lift on recent outcomes.
5. **Senior follow-up: the model ranks well but the campaign does not gain.** High
   propensity customers may buy anyway; test against random targeting and consider
   targeting the middle of the distribution or an uplift approach.

## Pitfalls

- Reporting accuracy on imbalanced data.
- Random train-test split on time-dependent data.

## Sources

- XGBoost, Introduction to Boosted Trees: <https://xgboost.readthedocs.io/en/stable/tutorials/model.html>
- Prokhorenkova et al., "CatBoost: unbiased boosting with categorical features" (2018): <https://arxiv.org/abs/1706.09516>
- scikit-learn, probability calibration: <https://scikit-learn.org/stable/modules/calibration.html>
- Optuna: <https://optuna.org/>
- SHAP documentation: <https://shap.readthedocs.io/en/latest/>
