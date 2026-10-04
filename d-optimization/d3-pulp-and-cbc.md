[Contents](../index.md) · D3 · P2

# PuLP and CBC

## In one minute

PuLP is a Python library for writing linear and mixed-integer models in readable code; it
does not solve anything itself but hands the model to a solver. CBC is the open-source
solver bundled with it. I chose them because they are free, simple to deploy and enough
for a model of this size; a commercial solver is faster on large or hard models but costs
a licence.

## Key ideas

- **Model in PuLP.**

  ```python
  import pulp

  m = pulp.LpProblem("allocation", pulp.LpMaximize)
  x = pulp.LpVariable.dicts("x", (sources, plants), lowBound=0)
  y = pulp.LpVariable.dicts("y", plants, cat="Binary")

  m += pulp.lpSum(margin[s][p] * x[s][p] for s in sources for p in plants)   # objective
  for s in sources:
      m += pulp.lpSum(x[s][p] for p in plants) <= supply[s]                  # constraint
  for p in plants:
      m += pulp.lpSum(x[s][p] for s in sources) <= capacity[p] * y[p]

  m.solve(pulp.PULP_CBC_CMD(timeLimit=60, gapRel=0.01, msg=False))
  pulp.LpStatus[m.status], pulp.value(m.objective), x["A"]["P1"].value()
  ```

- **Status.** Always check it: Optimal, Infeasible, Unbounded, Not Solved. A time limit
  can return a feasible but unproven solution.
- **Solver options.** Time limit, relative gap, threads, warm start.
- **Solver independence.** The same PuLP model runs on CBC, HiGHS, GLPK, Gurobi or CPLEX
  by changing the solver object.
- **CBC.** COIN-OR branch and cut. Free and adequate for small and medium models; slower
  and less robust than commercial solvers on hard ones.
- **HiGHS.** Newer open-source solver, generally faster than CBC; the default in SciPy.
- **Gurobi, CPLEX.** Commercial; much faster on hard MIPs, better diagnostics (for
  example an irreducible infeasible subset to explain infeasibility).
- **Alternatives to PuLP.** Pyomo (also nonlinear), OR-Tools (strong CP-SAT solver for
  scheduling and routing), `scipy.optimize.milp`.
- **Engineering around the model.** Separate data loading, model building and result
  extraction; validate inputs; log status, gap and solve time; export the model (`.lp`
  file) for debugging.

## On my CV

"(PuLP, CBC)" in the optimizer bullet; PuLP in Libraries.

## Likely questions

1. **Why PuLP and CBC?** Free, pure Python deployment, sufficient for the model's size;
   and the model can move to another solver unchanged.
2. **What would make you switch solver?** Solve time or gap not acceptable within the
   planning window, or a need for infeasibility diagnostics.
3. **How do you debug a wrong answer?** Write the `.lp` file, test on a tiny instance
   solvable by hand, check each constraint's units and direction.
4. **How do you handle a time limit?** Accept the incumbent with its reported gap, and
   show the gap to the user.
5. **Senior follow-up: how was it delivered to the planners?** Describe the interface
   (inputs they edit, outputs they read), and how they re-run scenarios.

## Pitfalls

- Reading variable values without checking the solve status.
- Building constraints in Python loops so slow that model build dominates solve time.

## Sources

- PuLP documentation: <https://coin-or.github.io/pulp/>
- CBC (COIN-OR branch and cut): <https://github.com/coin-or/Cbc>
- HiGHS: <https://highs.dev/>
