[Contents](../index.md) · G6 · P2

# Energy domain

## In one minute

Electric load is driven by the calendar and the weather, and repeats daily, weekly and
yearly, so it forecasts well from lags, calendar features and temperature. Solar output is
driven by the sun's position and by clouds: the clear-sky shape is predictable and the
cloud effect is not. A battery project uses both forecasts as inputs to an optimisation
that decides when to charge and discharge.

## Key ideas

- **Load drivers.** Hour of day, day of week, holidays (Songkran and New Year shift load
  sharply in Thailand), temperature and humidity (air conditioning), and for a single
  site its operating schedule.
- **Load features.** Lags at 24 and 168 hours, same hour previous days, temperature and
  its square or cooling degree hours, holiday flags.
- **Horizons.** Very short term (minutes to hours, operations), short term (day ahead,
  scheduling), medium and long term (planning).
- **Solar generation.**
  - Zero at night; bell-shaped on a clear day.
  - *Clear-sky model*: expected irradiance from location and time. Forecasting the ratio
    of actual to clear-sky output removes the predictable part.
  - Inputs: irradiance and cloud forecasts from numerical weather prediction, temperature
    (panels lose efficiency when hot), recent output.
  - Persistence (the last ratio continues) is a strong short-horizon baseline.
- **Metrics.** MAE or RMSE normalised by capacity; not MAPE for solar. Peak-hour error
  matters most for load.
- **Net load.** Load minus solar: what the grid or battery must supply.
- **Battery scheduling: forecast, then optimise.**
  - Decision: charge or discharge power per time step.
  - State of charge: $$\text{soc}_{t+1} = \text{soc}_t + \eta_c\, \text{charge}_t - \text{discharge}_t / \eta_d$$, within
    capacity; power limits.
  - Objectives: shift solar energy to the evening (self-consumption), cut the peak
    (demand charge), buy when the tariff is low (time-of-use arbitrage).
  - A linear or mixed-integer programme (binary to forbid charging and discharging at
    once).
- **Forecast error in the loop.** Re-optimise as new data arrive (rolling horizon);
  evaluate forecasts by the cost of the resulting schedule, not only by MAE.
- **Degradation.** Each cycle wears the battery; a cycle cost in the objective prevents
  pointless cycling.

## On my CV

"Built forecasting models for electric load and solar battery optimization projects"
(VISTEC/VISAI). My part was the forecasting models. My chemical engineering degree and
the shift engineer job at a power producer are relevant background here.

**To fill in (only I know):** the site type and horizon, the features that mattered, the
accuracy against baseline, and who built the optimisation.

## Likely questions

1. **What drives load?** Calendar and temperature, plus site-specific schedules.
2. **Why is solar harder?** Clouds. The deterministic part is easy; the forecast is only
   as good as the weather forecast.
3. **How did the forecast feed the battery decision?** As input to the schedule
   optimisation, re-run as forecasts update.
4. **How wrong can the forecast be before the battery schedule loses money?** Explain a
   sensitivity analysis on schedule cost.
5. **Senior follow-up: where would you spend effort, forecast or optimiser?** Wherever
   the schedule's cost is most sensitive; often peak timing rather than average error.

## Pitfalls

- Reporting MAPE on solar.
- Training on measured weather and predicting with forecast weather without noting it.

## Sources

- Hong and Fan, "Probabilistic electric load forecasting: A tutorial review" (2016): <https://research.monash.edu/en/publications/probabilistic-electric-load-forecasting-a-tutorial-review/>
- pvlib, clear-sky models: <https://pvlib-python.readthedocs.io/en/stable/user_guide/modeling_topics/clearsky.html>
- Hyndman and Athanasopoulos, *Forecasting: Principles and Practice*, complex seasonality (electricity demand examples): <https://otexts.com/fpp3/complexseasonality.html>
