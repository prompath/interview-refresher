[Contents](../index.md) · B2 · P1

# Recommender evaluation

## In one minute

Offline, I hold out each customer's most recent interactions, ask the model for a top-k
list from the earlier data, and score how well the list recovers what they actually took,
with ranking metrics. Offline metrics only say the model predicts past behaviour; whether
recommendations *change* behaviour needs an online test against a control.

## Key ideas

- **Split by time.** Train on the past, test on the future. Random splits leak.
- **Metrics at k.**

  ```
  precision@k = relevant in top k / k
  recall@k    = relevant in top k / all relevant
  hit rate@k  = share of users with at least one relevant item in top k
  ```

- **Rank-aware metrics.**
  - *MRR*: mean of 1 / rank of the first relevant item.
  - *MAP*: mean over users of average precision (precision at each relevant position).
  - *NDCG@k*: gain discounted by log of position, divided by the best possible ordering;
    handles graded relevance.
- **Beyond accuracy.** Coverage (share of catalogue ever recommended), diversity,
  novelty, and fairness across segments.
- **Baselines.** Most popular, and "same as last time". A model that cannot beat
  popularity is not worth deploying.
- **Why offline and online disagree.**
  - Logged data reflect what the old system showed (exposure bias).
  - Offline rewards predicting what customers would do anyway; the business wants
    incremental purchases.
  - Business rules alter the list after the model.
- **Online.** A/B test of recommender against control or the previous version, on
  conversion and revenue per customer; see [A1](../a-experimentation/a1-ab-test-design.md).
- **Evaluate after rules.** Score the list the customer actually receives, not the raw
  model output.

## On my CV

Supports "package recommender" and "Built presale proofs of concept for recommendation
systems" (Sertis). For a small catalogue with one or a few offers per customer, hit rate
and precision at small k matter more than NDCG at 10.

## Likely questions

1. **Which metric would you pick?** Depends on the surface: one offer per call means
   hit rate@1 or precision@1; a ranked list means NDCG.
2. **Precision or recall?** Precision when slots are scarce (one call, one offer); recall
   when generating candidates for a later ranker.
3. **Offline improved, online did not. Why?** The model learned to predict organic
   behaviour, or rules removed the improved items, or the test was underpowered.
4. **How do you evaluate with implicit feedback?** Treat held-out interactions as
   relevant; accept that unobserved is not the same as irrelevant, so absolute values are
   pessimistic and only comparisons matter.
5. **Senior follow-up: what would you report to the business?** Incremental conversion
   and revenue from the online test, with offline metrics kept as an engineering check.

## Pitfalls

- Reporting accuracy or AUC for a top-k problem.
- Tuning on the test period.

## Sources

- Google, Recommendation Systems course: <https://developers.google.com/machine-learning/recommendation>
- Evaluation measures in information retrieval (precision@k, MAP, NDCG): <https://en.wikipedia.org/wiki/Evaluation_measures_(information_retrieval)>
- Spark MLlib ranking metrics: <https://spark.apache.org/docs/latest/mllib-evaluation-metrics.html#ranking-systems>
