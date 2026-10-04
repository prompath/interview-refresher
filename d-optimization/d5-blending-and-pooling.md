[Contents](../index.md) · D5 · P3

# Blending and pooling problems

## In one minute

A blending problem mixes inputs of known composition to make products that meet quality
limits at least cost; it is a linear programme. A pooling problem adds intermediate tanks
where inputs mix before being sent on, so the composition of what leaves a tank is itself a
variable. Flow times composition is a product of two variables, which makes the problem
bilinear and non-convex.

## Key ideas

- **Blending (linear).** Inputs $$i$$ with known quality $$q_i$$; amounts $$x_i$$:

  $$
  \sum_i q_i\, x_i \le q_{\max} \sum_i x_i \qquad \text{(quality limit on the blend)}
  $$

  Linear because $$q_i$$ is data. The classic examples are diet, feed mix and fuel
  blending.
- **Pooling (bilinear).** Sources → pools → products. Pool quality $$p$$ is unknown:

  $$
  p \cdot \text{outflow} = \sum_i q_i \cdot \text{inflow}_i
  $$

  $$p \cdot \text{outflow}$$ multiplies two variables. Many local optima; no guarantee from an LP
  solver.
- **Ways to handle pooling.**
  - Fix the pool compositions or the split fractions and solve an LP; iterate
    (successive linear programming).
  - Discretise one variable and use binaries (a MIP approximation).
  - McCormick envelopes: linear relaxation of each bilinear term, giving bounds.
  - A global nonlinear solver (spatial branch and bound).
- **My problem.** Sources go straight to plants with given composition and efficiency, so
  production is linear in the flows. It would become a pooling problem if sources were
  mixed in a common header before the plants and plant performance depended on that mix.

## On my CV

Background to the gas allocation optimizer. Useful when an interviewer with a process
industry background asks "isn't that non-linear?".

## Likely questions

1. **Why is your model linear?** Compositions and efficiencies are inputs, not decisions.
2. **What would make it non-linear?** Mixing before processing with composition-dependent
   yield.
3. **How would you solve it then?** Start with fixed-fraction iteration or discretisation,
   and move to a global solver only if the gap matters.
4. **Senior follow-up: how do you decide how much realism to model?** Enough to change
   the decision. Compare the simplified model's plan with what the plant can actually
   run, and add detail where they differ.

## Pitfalls

- Claiming the model is exact where an assumption (fixed efficiency) made it linear. Say
  the assumption.

## Sources

- PuLP, a blending problem: <https://coin-or.github.io/pulp/CaseStudies/a_blending_problem.html>
- Gupte et al., "Relaxations and discretizations for the pooling problem": <https://www2.isye.gatech.edu/~sahmed/PoolingNewDiscrete.pdf>
- McCormick envelopes: <https://optimization.cbe.cornell.edu/index.php?title=McCormick_envelopes>
