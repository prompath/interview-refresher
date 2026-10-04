[Contents](../index.md) · J8 · P2

# Trade-off judgement

## In one minute

Senior interviews probe judgement with "it depends" questions. A good answer names the
criteria, says which way I lean by default and why, and what would change my mind. My
defaults: the simplest thing that meets the need, measured against a baseline, with
complexity added only when a test shows it pays.

## Key ideas

- **Simple versus complex model.**
  - Default simple: easier to explain, debug, maintain and retrain.
  - Go complex when the measured gain is worth the running cost and the team can support
    it.
  - Question to ask: what does one point of accuracy earn?
- **Accuracy versus interpretability.** Regulated or contested decisions need
  explanation; ranking for a campaign needs less. Post-hoc explanation (SHAP) narrows
  the gap but is not the same as a transparent model.
- **Build versus buy (vendor).**
  - Buy when the capability is not core, the vendor is clearly ahead, and time matters.
  - Build when it is core, needs deep integration with internal data, or lock-in is
    costly.
  - Either way keep measurement in-house: an independent holdout to judge the vendor.
- **Speed versus rigour.** Reversible, low-cost decisions can go on thin evidence;
  irreversible or costly ones need a proper test. Say which kind it is.
- **Rules versus models.** Rules are transparent and immediate; models scale and adapt.
  Often rules first, then a model inside the rules.
- **Batch versus real time.** Real time only where freshness changes the decision.
- **Explore versus exploit.** Some budget for exploration (random group, new offers) is
  the price of future learning.
- **Short-term versus long-term metric.** Conversion now against revenue, churn and
  customer experience later; guardrails and holdouts protect the long term.
- **New work versus maintenance.** Unmaintained models decay; reserve capacity.
- **Perfect data versus starting.** Start with what exists if the baseline can be
  measured; fix data where it blocks.
- **How to present a trade-off.** Options, criteria, recommendation, what I would watch
  to revisit it. Then let the owner decide.

## My evidence

Maintaining a bandit beside simpler monthly models and testing one against the other;
working with vendors while keeping the control group in-house; choosing an open-source
solver adequate for the problem; keeping business rules explicit around a model.

## Likely questions

1. **When would you choose logistic regression over boosting?** Small data, need for
   explanation, or no measurable gain from boosting.
2. **Should we buy this vendor's model?** Depends on the criteria above; insist on an
   independent test.
3. **How much evidence is enough to ship?** By reversibility and cost of being wrong.
4. **Tell me about a decision you would make differently now.** A prepared story.
5. **Lead-level follow-up: the team wants to rebuild a working system with newer
   technology.** Ask what problem it solves, what it costs, and whether a smaller change
   gets most of the benefit.

## Pitfalls

- "It depends" with no default and no criteria.
- Arguing for complexity because it is interesting.

## Sources

- Zinkevich, "Rules of Machine Learning": <https://developers.google.com/machine-learning/guides/rules-of-ml>
- Rudin, "Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead" (2019): <https://arxiv.org/abs/1811.10154>
- Sculley et al., "Hidden Technical Debt in Machine Learning Systems" (2015): <https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems>
