[Contents](../index.md) · D2 · P1

# Linear and mixed-integer programming

## In one minute

A linear programme maximises a linear objective subject to linear constraints over
continuous variables, and is solved quickly and exactly. A mixed-integer programme requires
some variables to be whole numbers, which makes it hard in general. Solvers handle it with
branch and bound: solve the problem with the integer requirement relaxed, then split on a
fractional variable and repeat, discarding branches that cannot beat the best solution
found.

## Key ideas

- **Linear programme.** $$\max\; c^\top x \ \text{ subject to } \ Ax \le b,\ x \ge 0$$. The feasible region is a convex
  polytope; an optimum lies at a vertex.
- **Solving LPs.** Simplex walks along vertices; interior-point methods cut through the
  inside. Both are fast in practice.
- **Duality.** Every LP has a dual; at the optimum, objectives are equal. The dual value
  (shadow price) of a constraint is how much the objective improves per unit of
  relaxation.
- **Why integers are hard.** The feasible set is no longer convex; rounding an LP solution
  can be infeasible or far from optimal. The problem class is NP-hard.
- **LP relaxation.** Drop integrality. Its optimum is an upper bound (for maximisation) on
  the integer optimum.
- **Branch and bound.**
  1. Solve the relaxation.
  2. If the solution is integral, it is a candidate (the *incumbent*).
  3. Otherwise pick a fractional variable and create two subproblems ($$x \le \lfloor v \rfloor$$,
     $$x \ge \lceil v \rceil$$).
  4. Prune a subproblem if it is infeasible or its bound is no better than the incumbent.
- **Cutting planes.** Extra valid inequalities that cut off fractional solutions and
  tighten the relaxation. Branch and cut combines both.
- **MIP gap.**

  $$
  \text{gap} = \frac{\lvert \text{best bound} - \text{incumbent} \rvert}{\lvert \text{incumbent} \rvert}
  $$

  The solver stops at a tolerance; a 1% gap means the answer is proven within 1% of
  optimal.
- **Formulation strength.** Two correct formulations can differ hugely in solve time; a
  tighter relaxation (small big-M values, fewer symmetries) is faster.
- **Heuristics.** Solvers use them to find good incumbents early; metaheuristics (genetic
  algorithms, simulated annealing) give answers without a bound.

## On my CV

"Mixed-integer optimization" in Skills and Summary; the gas allocation optimizer.

## Likely questions

1. **LP versus MIP?** Continuous versus some integer variables; polynomial in practice
   versus NP-hard.
2. **Explain branch and bound.** As above, with the role of bounds in pruning.
3. **What is the MIP gap and what did you set?** Distance between the best solution and
   the best possible; set by how much precision the business decision needs.
4. **Why not round the LP solution?** It may violate constraints or be far from optimal,
   especially for binary decisions.
5. **Senior follow-up: optimisation or machine learning?** Optimisation when the rules of
   the system are known and the task is to choose; machine learning when a quantity must
   be predicted. Often both: forecast, then optimise.

## Pitfalls

- Saying the solver "tries all combinations".
- Confusing a heuristic's answer with a proven optimum.

## Sources

- Gurobi, "Mixed-Integer Programming (MIP): The Complete FAQ Guide": <https://www.gurobi.com/resources/faq/mixed-integer-programming-mip>
- Branch and bound: <https://en.wikipedia.org/wiki/Branch_and_bound>
- Linear programming (duality, simplex): <https://en.wikipedia.org/wiki/Linear_programming>
