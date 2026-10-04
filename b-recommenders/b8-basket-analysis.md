[Contents](../index.md) · B8 · P3

# Basket analysis

## In one minute

Market basket analysis finds products that are bought together more often than chance
would give, as rules of the form "if A then B". It needs only transaction data, is easy
to explain, and makes a quick proof of concept for cross-sell before a full recommender.

## Key ideas

- **Measures for a rule A → B.**

  $$
  \begin{aligned}
  \text{support}(A, B) &= P(A \cap B) \\
  \text{confidence}(A \to B) &= P(B \mid A) = \frac{\text{support}(A, B)}{\text{support}(A)} \\
  \text{lift}(A \to B) &= \frac{P(B \mid A)}{P(B)}
  \end{aligned}
  $$

  Lift above 1 means A and B occur together more than if independent. High confidence
  with lift near 1 just means B is popular.
- **Apriori.** Find frequent itemsets level by level; any superset of an infrequent set is
  infrequent, so it can be pruned. Many passes over the data.
- **FP-growth.** Compresses transactions into a prefix tree and mines it without
  generating candidates; faster on large data (available in Spark ML).
- **Thresholds.** Minimum support removes rare noise but also rare valuable items;
  minimum confidence and lift filter the rules.
- **Limits.** No personalisation, no order or time, many redundant rules, and popular
  items dominate. Rules are associations, not causes.
- **Use.** Bundles, shelf or page placement, "frequently bought together", and a baseline
  for a recommender.

## On my CV

"Built presale proofs of concept for recommendation systems, including basket analysis"
(Sertis). A proof of concept for a prospective client, not a production system.

## Likely questions

1. **Confidence versus lift?** Confidence ignores how common B is; lift corrects for it.
2. **Why Apriori's pruning works?** Support can only fall as items are added to a set.
3. **When would you use this over collaborative filtering?** Small data, a need for
   explainable rules, or a quick first result.
4. **How would you validate a rule?** Hold-out period, then an experiment on the placement
   or bundle.
5. **Senior follow-up: what did the proof of concept need to show the client?** That
   their data supports useful, non-obvious associations, and what a production system
   would add.

## Pitfalls

- Presenting high-confidence rules whose lift is about 1.

## Sources

- mlxtend, association rules: <https://rasbt.github.io/mlxtend/user_guide/frequent_patterns/association_rules/>
- Spark ML frequent pattern mining (FP-growth): <https://spark.apache.org/docs/latest/ml-frequent-pattern-mining.html>
- Association rule learning: <https://en.wikipedia.org/wiki/Association_rule_learning>
