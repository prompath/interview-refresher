[Contents](../index.md) · G3 · P1

# Forecast evaluation

## In one minute

I evaluate a forecaster by backtesting: train on data up to a date, forecast the next
horizon, move the date forward and repeat, then average the errors. The metric follows the
decision: MAE or RMSE in real units when one series matters, a scaled metric such as MASE
to compare across series. Every result is shown next to a naive baseline.

## Key ideas

- **Time series cross-validation.** Never shuffle.
  - *Expanding window*: training set grows with each fold.
  - *Sliding window*: fixed-length training set moves forward.
  The test block has the same length as the real forecast horizon; leave a gap if data
  arrive late in production.
- **Metrics.**

  ```
  MAE   = mean |y − ŷ|
  RMSE  = sqrt( mean (y − ŷ)² )              penalises large errors
  MAPE  = mean |y − ŷ| / |y|                 undefined at y = 0, favours under-forecasts
  sMAPE = mean 2|y − ŷ| / (|y| + |ŷ|)        bounded, still unstable near zero
  MASE  = MAE / MAE of the naive forecast in-sample     < 1 beats naive
  ```

- **Which metric.**
  - MAE: median-like, robust.
  - RMSE: when large errors cost more (peak load).
  - MAPE: easy to explain, wrong for series near zero (solar at night).
  - MASE or weighted MAPE: across series of different scale.
- **Bias.** Mean error; a forecast can have low MAE and still be consistently high.
- **By horizon.** Error at step 1 and step 24 differ; report per horizon.
- **Probabilistic.** Pinball (quantile) loss, interval coverage (does the 90% interval
  hold 90% of actuals?), CRPS.
- **Baselines.** Naive, seasonal naive. Report skill relative to them.
- **Residual checks.** Errors should have no remaining pattern by hour, weekday or level.
- **Is the difference real?** Compare over several folds; Diebold-Mariano test for two
  forecasters.
- **Model selection without leakage.** Tune on validation folds; keep a final period
  untouched.
- **Business metric.** The forecast feeds a decision (battery schedule, purchase). The
  cost of that decision under forecast error is the real score.

## On my CV

The AutoML pipeline had to choose between models automatically, so its evaluation design
was the core of it. sktime provides the splitters (`ExpandingWindowSplitter`,
`SlidingWindowSplitter`) and metrics.

## Likely questions

1. **Why not k-fold?** It trains on the future to predict the past.
2. **Why is MAPE a problem for solar?** Division by zero or tiny values at night and
   dawn; use MAE, normalised by capacity.
3. **Your model has 5% MAPE. Is that good?** Compared with seasonal naive on the same
   folds, and at which horizon?
4. **Expanding or sliding window?** Expanding when all history helps; sliding when old
   data are no longer representative.
5. **Senior follow-up: accuracy improved but users see no benefit.** The metric did not
   match the decision; evaluate on the cost of decisions made from the forecast.

## Pitfalls

- One train-test split treated as the result.
- Tuning and reporting on the same folds.

## Sources

- Hyndman and Athanasopoulos, *Forecasting: Principles and Practice*, evaluating accuracy and time series cross-validation: <https://otexts.com/fpp3/accuracy.html>
- Hyndman and Koehler, "Another look at measures of forecast accuracy" (MASE): <https://robjhyndman.com/papers/mase.pdf>
- sktime documentation (splitters and performance metrics): <https://www.sktime.net/en/stable/>
