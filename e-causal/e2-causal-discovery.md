[Contents](../index.md) · E2 · P2

# Causal discovery

## In one minute

Causal discovery tries to learn the causal graph from data instead of assuming it.
Constraint-based algorithms such as PC test which variables are independent given others
and draw the graphs consistent with those results. The output is usually a set of
equivalent graphs with some arrows undirected, and it rests on strong assumptions, so I
treat it as a source of hypotheses to check with domain experts, not as proof.

## Key ideas

- **Assumptions.**
  - *Causal Markov*: each variable is independent of its non-descendants given its
    parents.
  - *Faithfulness*: every independence in the data comes from the graph structure, not
    from effects cancelling out.
  - *Causal sufficiency*: no unmeasured common causes (needed by PC, not by FCI).
  - Acyclicity; correct independence tests; enough data.
- **PC algorithm.**
  1. Start with a complete undirected graph.
  2. Remove an edge when two variables are independent given some subset of neighbours,
     with growing subset size (the *skeleton*).
  3. Orient colliders `X → Z ← Y` where `X` and `Y` are non-adjacent and `Z` was not in
     their separating set.
  4. Propagate orientations with rules that avoid new colliders and cycles.
- **Output.** A CPDAG: the Markov equivalence class. Undirected edges mean the data
  cannot tell the direction.
- **FCI.** Allows hidden confounders; output is a partial ancestral graph with more edge
  types, including "possibly confounded".
- **GES.** Score-based: greedily adds then removes edges to maximise a score such as BIC.
- **Functional methods.** LiNGAM assumes linear relations with non-Gaussian noise and can
  orient all edges.
- **Independence tests.** Fisher's z (linear Gaussian), chi-square or G² (discrete),
  kernel tests (general, slow). The choice matters with mixed data.
- **causal-learn.** Python library (from the CMU group behind Tetrad) with PC, FCI, GES,
  LiNGAM and the tests; background knowledge can forbid or require edges.
- **Practical limits.** Sensitive to sample size, test choice and significance level;
  errors in early tests propagate; results change with the variables included.
- **Using background knowledge.** Time order (tenure cannot be caused by resignation) and
  domain rules cut the search and fix directions.
- **From graph to effect.** Discovery gives structure; estimating how large an effect is
  needs the methods in [E1](e1-causal-inference-basics.md).

## On my CV

causal-learn in Libraries; used in the Sertis attrition proof of concept.

## Likely questions

1. **How does PC decide there is no edge?** It finds a conditioning set that makes the two
   variables independent.
2. **Why are some edges undirected?** Different graphs imply the same independencies.
3. **How much do you trust the result?** As hypotheses. I check stability (bootstrap the
   data, vary alpha) and review with domain experts.
4. **PC versus FCI?** FCI when hidden common causes are plausible, at the cost of a less
   specific graph.
5. **Senior follow-up: what did the client get from it?** A ranked set of plausible
   drivers to act on or test, clearer than a feature-importance chart, with caveats
   stated.

## Pitfalls

- Presenting a discovered graph as established fact.
- Ignoring hidden confounders with PC.

## Sources

- causal-learn documentation: <https://causal-learn.readthedocs.io/en/latest/>
- Zheng et al., "Causal-learn: Causal Discovery in Python" (2023): <https://arxiv.org/abs/2307.16405>
- Glymour, Zhang, Spirtes, "Review of Causal Discovery Methods Based on Graphical Models" (2019): <https://www.frontiersin.org/articles/10.3389/fgene.2019.00524/full>
