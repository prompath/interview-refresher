[Contents](../index.md) · B1 · P1

# Collaborative filtering

## In one minute

Collaborative filtering recommends items from the behaviour of similar users, with no need
for item descriptions: customers who behaved alike in the past will want similar things.
The two main forms are neighbourhood methods (item-to-item similarity) and matrix
factorisation (learn a short vector per user and per item whose dot product predicts
preference). In telecom the "ratings" are implicit: which package a customer holds or
bought, not a score.

## Key ideas

- **Explicit versus implicit feedback.** Explicit: ratings. Implicit: purchases, usage,
  clicks. Implicit data has no negatives; a missing entry means "unknown", not "disliked".
- **Item-based neighbourhood.** Similarity between item columns (cosine, Jaccard);
  recommend items similar to what the user has. Easy to explain and stable.
- **Matrix factorisation.** Approximate the user × item matrix $$R \approx U V^\top$$ with $$k$$
  latent factors. Score = $$u_i \cdot v_j$$.
- **ALS for implicit feedback.** Treat every cell as a preference (1 if interacted, else 0) with a confidence
  weight $$c = 1 + \alpha r$$ that grows with interaction strength; alternate between solving
  for users with items fixed and the reverse. Each step is a least-squares problem and
  parallelises well (Spark ML's `ALS` with `implicitPrefs=True`).
- **Hyperparameters.** Rank $$k$$, regularisation, confidence scale $$\alpha$$, iterations.
- **Cold start.** New users or items have no interactions. Fall back to popularity,
  segment rules or content features.
- **Popularity bias.** Models over-recommend popular items; check coverage and
  per-segment results.
- **Small catalogues.** With tens of packages rather than millions of items, the model
  matters less than eligibility rules and the candidate set, and a simpler model is
  often enough.
- **Beyond CF.** Content-based and hybrid models; two-tower neural models; sequence
  models. Know the names.

## On my CV

"Adjusted and extended the package recommender and its business rules with the business
team, and made it production-ready." The recommender is a collaborative-filtering model
with business rules on top. I inherited the model and extended the rules and pipeline; I
did not invent the model.

## Likely questions

1. **User-based or item-based?** Item-based: items are fewer and more stable than users,
   so similarities are cheaper and less noisy.
2. **How does implicit ALS differ from rating prediction?** It fits all cells with
   confidence weights rather than only the observed ratings.
3. **How do you handle a new customer?** Popular or rule-based default for their segment
   until behaviour accumulates.
4. **Why collaborative filtering for a small catalogue?** It captures which packages
   similar customers moved to; but I would compare it with a simple classifier or
   transition table as a baseline.
5. **Senior follow-up: how would you improve it?** First measure where it loses:
   candidates removed by rules, ranking quality, or offer acceptance. Then choose between
   better features (a supervised ranker), better rules, or better exploration.

## Pitfalls

- Treating missing interactions as negatives without weighting.
- Evaluating on random splits that leak future behaviour; split by time.

## Sources

- Hu, Koren, Volinsky, "Collaborative Filtering for Implicit Feedback Datasets" (2008): <http://yifanhu.net/PUB/cf.pdf>
- Spark ML collaborative filtering (ALS): <https://spark.apache.org/docs/latest/ml-collaborative-filtering.html>
- Google, Recommendation Systems course: <https://developers.google.com/machine-learning/recommendation>
