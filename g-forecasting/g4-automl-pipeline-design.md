[Contents](../index.md) · G4 · P1

# AutoML pipeline design

## In one minute

An AutoML system for forecasting takes a series and a horizon and returns a fitted model
without a data scientist in the loop. Inside it is a search: a set of candidate pipelines
(preprocessing plus model plus hyperparameters), a backtest that scores each candidate,
a search strategy that decides what to try next within a time budget, and a final refit of
the winner. The design work is in the search space, the evaluation, and making it robust
to messy input.

## Key ideas

- **Stages.**
  1. *Ingest and validate*: frequency detection, missing timestamps, duplicates, outliers.
  2. *Preprocess*: imputation, transforms (log, differencing, deseasonalising), feature
     generation.
  3. *Candidates*: naive baselines, ETS, ARIMA, Prophet, reduction with boosting, neural
     models.
  4. *Evaluate*: time series cross-validation with a chosen metric.
  5. *Search*: over models and hyperparameters under a budget.
  6. *Select and refit* on all data; optionally ensemble the top few.
  7. *Serve*: store the model, forecast on request, retrain on a schedule.
- **Search strategies.**
  - *Grid*: exhaustive, explodes with dimensions.
  - *Random*: better coverage per trial than grid.
  - *Bayesian* (TPE, Gaussian process): models score as a function of parameters and
    samples promising regions.
  - *Successive halving / Hyperband*: give many candidates a small budget and keep the
    best.
- **Common interface.** sktime gives every forecaster `fit`, `predict` and a forecasting
  horizon, plus pipelines (`TransformedTargetForecaster`), tuning
  (`ForecastingGridSearchCV`) and model choice (`MultiplexForecaster`), so candidates are
  interchangeable.
- **Guardrails.** Always include baselines; fall back to seasonal naive if nothing beats
  it or everything fails; per-candidate timeouts; errors isolated per candidate.
- **Overfitting the validation.** Many candidates on few folds select by luck. Use
  several folds and prefer simpler models on ties.
- **Architecture.** API in front, job queue, workers that run the search, a store for
  data, models and run metadata; all packaged with Docker so it runs on one server.
- **Self-hosted.** Runs on own hardware instead of a public cloud: data stays in house,
  no managed services, so queueing, storage and monitoring are our own.
- **Existing tools to compare with.** AutoGluon-TimeSeries, Nixtla's statsforecast and
  mlforecast, AutoTS, cloud AutoML services.

## On my CV

"Designed and built a self-hosted automated machine learning (AutoML) pipeline for time
series forecasting." It was the company's attempt at an AutoML product, hosted on its own
server. It had no customers, and I claim no usage.

**To fill in (only I know):**

- Which candidates and search strategy were in it, and the evaluation scheme.
- The architecture: components, what ran in Docker, how a job flowed.
- Which parts were mine and which were colleagues'.
- What I learned from it not reaching customers.

## Likely questions

1. **Walk me through the architecture.** The stages and components above, with my part.
2. **How did it choose a model?** Backtest score on a stated metric, baselines included.
3. **How did you keep search time bounded?** Budget per job, timeouts, early stopping of
   weak candidates.
4. **How does it compare with existing tools?** Honest comparison; what it did that they
   did not, and the reverse.
5. **Senior follow-up: it had no customers. Why, and what would you do differently?**
   A straight answer about product fit and validation with users before building.

## Pitfalls

- Implying the product was in use.
- Describing it as only "trying many models" without the evaluation design.

## Sources

- sktime documentation: <https://www.sktime.net/en/stable/>
- Feurer and Hutter, "Hyperparameter Optimization" in *Automated Machine Learning* (2019): <https://www.automl.org/book/>
- AutoGluon-TimeSeries: <https://auto.gluon.ai/stable/tutorials/timeseries/index.html>
