[Contents](../index.md) · H1 · P1

# Machine learning fundamentals

## In one minute

Supervised learning fits a function from features to a target on past data so that it
predicts well on new data. Everything else follows from that goal: hold data out to
estimate performance on new data, control model complexity to balance underfitting and
overfitting, choose a metric that matches the decision, and keep information from the
future or the target out of the features.

## Key ideas

- **Bias and variance.** Too simple a model misses the pattern (bias, underfitting); too
  flexible a model fits noise (variance, overfitting). Training error keeps falling with
  complexity; validation error falls and then rises.
- **Regularisation.**
  - *L2 (ridge)*: shrinks coefficients smoothly.
  - *L1 (lasso)*: drives some to zero, selecting features.
  - For trees: depth, minimum samples per leaf, learning rate, subsampling.
  - Early stopping; dropout for neural networks.
- **Validation.** Train, validation and test sets. k-fold cross-validation for small
  data; stratified for imbalanced classes; grouped when rows of one customer must stay
  together; time-based when the data are ordered in time.
- **Linear and logistic regression.** Coefficients as effects holding others fixed;
  logistic outputs log-odds; need scaling for regularisation; baseline for everything.
- **Decision trees.** Split to reduce impurity (Gini, entropy) or variance. Interpretable,
  unstable alone.
- **Bagging and random forest.** Many deep trees on bootstrap samples with random feature
  subsets, averaged. Reduces variance.
- **Boosting.** Shallow trees added in sequence, each fitting the errors of the ensemble
  so far. Reduces bias; needs a learning rate and early stopping.
- **Classification metrics.**

  $$
  \text{precision} = \frac{TP}{TP + FP} \qquad \text{recall} = \frac{TP}{TP + FN} \qquad F_1 = \frac{2 \cdot \text{precision} \cdot \text{recall}}{\text{precision} + \text{recall}}
  $$

  ROC AUC: probability a random positive is ranked above a random negative. PR AUC for
  rare positives. Log loss for probability quality. The threshold is a business choice.
- **Regression metrics.** MAE, RMSE, R².
- **Imbalance.** Right metric first; then class weights; resampling last, with
  recalibration.
- **Leakage.** Target information in features, preprocessing fitted on all data,
  duplicates across train and test, future data. Pipelines fitted inside each fold
  prevent the second.
- **Feature work.** Encoding categoricals (one-hot, target encoding with care), missing
  values, scaling for linear and distance models, interactions.
- **Interpretation.** Permutation importance, partial dependence, SHAP.
- **Unsupervised by name.** k-means, hierarchical clustering, PCA.

## On my CV

Underlies every model bullet; scikit-learn and XGBoost in Libraries. I also taught this
material to 200+ students, so I should explain it cleanly.

## Likely questions

1. **Explain overfitting and how you detect it.** Training score far better than
   validation; fix with regularisation, more data or a simpler model.
2. **Random forest versus gradient boosting?** Parallel averaged trees (variance
   reduction) versus sequential corrective trees (bias reduction); boosting is usually
   more accurate and more sensitive to tuning.
3. **Precision or recall?** Depends on the cost of each error; give an example from a
   calling campaign.
4. **L1 versus L2?** Sparsity versus smooth shrinkage.
5. **Senior follow-up: a junior shows 99% accuracy.** Ask about class balance, leakage
   and the split before anything else.

## Pitfalls

- Fitting scalers or encoders before splitting.
- Choosing the metric after seeing results.

## Sources

- scikit-learn user guide: <https://scikit-learn.org/stable/user_guide.html>
- Hastie, Tibshirani, Friedman, *The Elements of Statistical Learning*: <https://hastie.su.domains/ElemStatLearn/>
- Google, Machine Learning Crash Course: <https://developers.google.com/machine-learning/crash-course>
