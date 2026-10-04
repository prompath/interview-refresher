[Contents](../index.md) · G2 · P1

# Machine learning for forecasting

## In one minute

Forecasting becomes a regression problem once each time point is described by features
known at prediction time: past values (lags), rolling statistics, calendar fields and
external variables such as weather. Gradient boosting on such a table is a strong default.
The care is all in building features without using the future and in deciding how to
forecast several steps ahead.

## Key ideas

- **Reduction.** Slide a window over the series: features = last `w` values, target = the
  next one. sktime calls this *reduction* and wraps any scikit-learn regressor.
- **Features.**
  - *Lags*: `y_{t−1}`, `y_{t−24}`, `y_{t−168}` for hourly data.
  - *Rolling*: mean, min, max, standard deviation over past windows.
  - *Calendar*: hour, day of week, month, holiday; cyclical encoding with sine and cosine.
  - *Exogenous*: temperature, price, promotions. Future values must be *known or
    forecast* at prediction time.
- **Multi-step strategies.**
  - *Recursive*: one one-step model; feed predictions back. Errors accumulate.
  - *Direct*: one model per horizon. No accumulation, more models, each ignores the
    others.
  - *Multi-output*: one model predicts the whole horizon.
  - *DirRec* and hybrids combine them.
- **Trees cannot extrapolate.** A tree predicts within the range it saw. For trending
  series, difference or detrend first, or model the ratio to a baseline.
- **Global versus local.** Local: one model per series. Global: one model trained across
  many series, with series identifiers or static features; learns shared patterns and
  works for short series.
- **Leakage.** Rolling features must end before the forecast origin; scalers fitted on
  the training window only; lags shorter than the horizon are unavailable for direct
  forecasts.
- **Target transforms.** Log or Box-Cox for multiplicative variance; invert carefully.
- **Probabilistic forecasts.** Quantile loss gives prediction intervals from boosting.
- **Hierarchy.** Forecasts at different aggregation levels should add up
  (reconciliation).

## On my CV

"Built forecasting models for electric load and solar battery optimization projects" and
the AutoML pipeline. sktime and XGBoost are in Libraries.

## Likely questions

1. **How do you turn a series into a supervised problem?** Windowed lag features with the
   next value as target.
2. **Recursive or direct?** Recursive for short horizons and simplicity; direct when
   errors compound or horizons differ in behaviour. Compare on a backtest.
3. **Why did the boosted model flatten on a growing series?** It cannot predict beyond
   the training range; detrend or difference.
4. **How do you use weather when forecasting tomorrow?** With weather *forecasts*, and
   train on forecasts or accept the mismatch; never on actuals that would not be known.
5. **Senior follow-up: hundreds of series. One model or many?** A global model first,
   with per-series checks; local models where a series behaves differently.

## Pitfalls

- Rolling features that include the target period.
- Random cross-validation on time series.

## Sources

- Hyndman and Athanasopoulos, *Forecasting: Principles and Practice*: <https://otexts.com/fpp3/>
- sktime documentation (reduction forecasters): <https://www.sktime.net/en/stable/>
- Bontempi et al., "Machine Learning Strategies for Time Series Forecasting" (multi-step strategies): <https://link.springer.com/chapter/10.1007/978-3-642-36318-4_3>
