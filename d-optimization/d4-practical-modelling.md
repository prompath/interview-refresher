[Contents](../index.md) · D4 · P2

# Practical modelling

## In one minute

Most of the work in an optimisation project is not the solver. It is turning what planners
actually do into constraints, making the model give a useful answer when the constraints
cannot all be met, keeping the formulation tight and well scaled, and earning the
planners' trust by reproducing and then improving on their own plans.

## Key ideas

- **Infeasibility.** Real inputs often conflict. Find the cause by relaxing constraint
  groups one at a time, or with a solver's irreducible infeasible subset.
- **Soft constraints.** Replace `out ≥ quota` with `out + short ≥ quota`, `short ≥ 0`,
  and subtract `penalty · short` in the objective. The model always returns a plan and
  shows what was missed. Penalties encode priorities.
- **Big-M.** Links a continuous variable to a binary: `x ≤ M · y`. Choose `M` as small as
  is valid (the real capacity); a huge `M` weakens the relaxation and causes numerical
  trouble.
- **Common linearisations.**
  - Fixed cost or minimum run: `L · y ≤ x ≤ U · y`.
  - Either-or constraints: one binary and big-M.
  - Product of a binary and a bounded continuous variable: three linear inequalities.
  - Piecewise-linear curves: segments with binaries or special ordered sets.
  - Absolute value and min-max: auxiliary variable.
- **Product of two continuous variables.** Not linear (see
  [D5](d5-blending-and-pooling.md)); fix one, discretise, or use a nonlinear solver.
- **Scaling.** Keep coefficients within a few orders of magnitude (choose units
  sensibly); otherwise tolerances bite.
- **Sensitivity.** In the LP (or the MIP with integers fixed), shadow prices tell which
  constraint is worth relaxing and by how much the margin would change. Scenario runs
  answer "what if supply drops 10%".
- **Multiple objectives.** Weighted sum, or optimise one and constrain the others
  (lexicographic).
- **Validation with users.** Back-test on past weeks; explain each difference from the
  human plan; many "errors" reveal unwritten rules that become constraints.
- **Stability.** Planners dislike plans that change completely for a small input change;
  penalise deviation from the previous plan if needed.

## On my CV

"Scoped and built" the optimizer: the scoping half of the sentence lives here.

## Likely questions

1. **The model says infeasible on Monday morning. What does the planner see?** With soft
   constraints, a plan plus the list of quotas missed and by how much.
2. **How do you pick penalty weights?** From business priority and real cost, tested on
   past cases, agreed with the planners.
3. **What is wrong with a very large M?** Weak relaxation, slower solve, and numerical
   error that can let a "zero" binary carry flow.
4. **How did you gain the planners' trust?** Reproduced their plans, explained the
   differences, added the missing rules, and showed margin on historical weeks.
5. **Senior follow-up: what would you do differently?** A candid answer about scoping,
   data quality or handover.

## Pitfalls

- Hard constraints everywhere, so the first bad input breaks the tool.
- Tuning the model to past data without planners reviewing the plans.

## Sources

- Williams, *Model Building in Mathematical Programming*: <https://www.wiley.com/en-us/Model+Building+in+Mathematical+Programming%2C+5th+Edition-p-9781118443330>
- Gurobi, "Dealing with big-M constraints": <https://docs.gurobi.com/projects/optimizer/en/current/concepts/numericguide/tolerances_scaling.html>
- Big M method: <https://en.wikipedia.org/wiki/Big_M_method>
