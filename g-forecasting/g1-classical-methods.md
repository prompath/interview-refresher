[Contents](../index.md) · G1 · P1

# Classical methods

## In one minute

A time series is trend plus seasonality plus noise. Classical models describe those parts
directly: exponential smoothing weights recent observations more, and ARIMA models the
series from its own past values and past errors after differencing to remove trend. They
are fast, need little data and give prediction intervals, so they are the baseline any
machine learning forecaster has to beat.

## Key ideas

- **Decomposition.** Trend, seasonal and remainder, additive or multiplicative (STL).
- **Stationarity.** Mean, variance and autocorrelation constant over time. ARIMA needs it;
  differencing ($$y_t - y_{t-1}$$, or seasonal $$y_t - y_{t-m}$$) and log transforms get
  there. Tests: ADF (null: non-stationary), KPSS (null: stationary).
- **ACF and PACF.** Autocorrelation at each lag, and autocorrelation with shorter lags
  removed. A PACF cut-off at lag p suggests AR(p); an ACF cut-off at lag q suggests MA(q).
  Spikes at multiples of m show seasonality.
- **ARIMA(p, d, q).** `p` autoregressive terms, `d` differences, `q` moving-average terms
  (past forecast errors).
- **SARIMA(p,d,q)(P,D,Q)m.** Adds seasonal terms at period `m`. SARIMAX adds external
  regressors.
- **Choosing orders.** Information criteria (AIC, AICc) and automatic search (auto-ARIMA);
  then check residuals look like white noise (Ljung-Box test).
- **Exponential smoothing (ETS).**
  - *Simple*: level only.
  - *Holt*: level and trend.
  - *Holt-Winters*: level, trend and seasonality.
  Smoothing parameters set how fast old data are forgotten.
- **Prophet.** Additive model with piecewise-linear trend, Fourier seasonality and
  holiday effects; convenient for business series with several seasonalities.
- **Multiple seasonality.** Hourly load has daily, weekly and yearly cycles; SARIMA
  handles one period well, so use TBATS, Prophet, Fourier terms or a machine learning
  model.
- **Baselines.** Naive (last value), seasonal naive (same time last period), drift.
- **Prediction intervals.** Come from the model's error variance and widen with horizon.

## On my CV

"Time series forecasting" in Summary and Skills; the AutoML pipeline and the load and
solar forecasting models (VISTEC/VISAI). Classical models were candidates in the pipeline
and the baselines for the rest.

## Likely questions

1. **What is stationarity and why does it matter?** Stable statistical properties; ARIMA's
   theory assumes it, and regressions on trending series give spurious fits.
2. **How do you pick p, d, q?** Difference until stationary, read ACF and PACF, confirm
   with AICc, check residuals.
3. **ARIMA or exponential smoothing?** Often similar; ETS is simpler for clear trend and
   seasonality, ARIMA for autocorrelation structure. Try both on a backtest.
4. **When do classical models beat machine learning?** Few series, short history, strong
   regular seasonality.
5. **Senior follow-up: the business wants one number. What about uncertainty?** Give the
   forecast with an interval and explain the decision each bound would lead to.

## Pitfalls

- Fitting ARIMA on a non-stationary series without differencing.
- Skipping the seasonal-naive baseline.

## Sources

- Hyndman and Athanasopoulos, *Forecasting: Principles and Practice* (3rd ed.): <https://otexts.com/fpp3/>
- statsmodels, time series analysis: <https://www.statsmodels.org/stable/tsa.html>
- Prophet documentation: <https://facebook.github.io/prophet/>
