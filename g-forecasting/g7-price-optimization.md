[Contents](../index.md) · G7 · P3

# Price optimization

## In one minute

Price optimisation has two parts: a demand model that predicts how many units sell at each
price, and an optimisation that picks the price maximising revenue or profit under
business constraints. The demand model depends on clean history of prices, quantities and
everything else that moved sales, which is why the preprocessing pipeline is a large share
of such a project.

## Key ideas

- **Price elasticity.**

  $$
  \text{elasticity} = \frac{\%\ \text{change in quantity}}{\%\ \text{change in price}}
  $$

  Below −1 (elastic): cutting price raises revenue. Between −1 and 0 (inelastic): raising
  price raises revenue.
- **Log-log demand model.** $$\log q = a + b \log p + \text{controls}$$; $$b$$ is the elasticity.
- **Controls.** Seasonality, promotions, holidays, stock-outs, competitor price,
  cross-effects from substitutes and complements (cannibalisation).
- **Endogeneity.** Prices are set in response to demand (raised when demand is high), so
  the naive estimate is biased. Remedies: price experiments, instruments (cost shocks),
  careful controls.
- **Optimisation.** Profit $$(p - \text{cost}) \cdot q(p)$$; constraints such as price ranges, price
  ladders, margin floors, limited changes per period, consistent pricing across related
  items.
- **Preprocessing pipeline: what it must handle.**
  - Transactions aggregated to a product × period grain.
  - Effective price after discounts, not list price.
  - Stock-outs: zero sales with no stock is censored demand, not zero demand.
  - Promotions and events flagged.
  - Missing periods filled explicitly; outliers and returns treated.
  - Product hierarchy and new or discontinued items.
  - Point-in-time correctness: only data known at the time.
- **Pipeline design.** Stages with defined input and output schemas, validation at each
  stage, idempotent runs, tests on small fixtures.
- **Evaluation.** Demand forecast accuracy, plausibility of elasticities (sign, size),
  and ultimately a price test.

## On my CV

"Designed and built the data preprocessing pipeline for a price optimization project"
(VISTEC/VISAI). My part was the pipeline, not the pricing model.

**To fill in (only I know):** the industry, the data sources, the hardest data problems
and how the pipeline handled them, and who used its output.

## Likely questions

1. **What did the pipeline do?** Sources → cleaning → aggregation → features, with the
   specific problems it solved.
2. **Why is elasticity hard to estimate from history?** Price was not set at random.
3. **How do you treat stock-outs?** As censored demand: exclude or model them, never as
   true zeros.
4. **How did you test the pipeline?** Schema and range checks, unit tests on
   transformations, reconciliation of totals with the source.
5. **Senior follow-up: how would you validate the recommended prices?** A controlled
   price test on a subset of products or stores.

## Pitfalls

- Claiming the pricing model.

## Sources

- Price elasticity of demand: <https://en.wikipedia.org/wiki/Price_elasticity_of_demand>
- Phillips, *Pricing and Revenue Optimization* (2nd ed.): <https://www.sup.org/books/business/pricing-and-revenue-optimization>
- Facure, *Causal Inference for the Brave and True* (price elasticity as a causal problem): <https://matheusfacure.github.io/python-causality-handbook/landing-page.html>
