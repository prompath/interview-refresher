[Contents](../index.md) · D1 · P1

# Formulating the gas allocation problem

## In one minute

Each week, natural gas from three sources with different compositions must be split among
four processing plants that extract components at different efficiencies. The optimizer
chooses how much of each source goes to each plant so that every component's quota is met
and total margin is highest. Flows are continuous variables; on-off or stepwise operating
decisions are what make it mixed-integer.

## Key ideas

- **Sets.** Sources $$s$$ (3), plants $$p$$ (4), components $$c$$ (for example ethane, propane,
  heavier liquids).
- **Decision variables.** $$x_{s,p} \ge 0$$: volume from source $$s$$ to plant $$p$$ in the week.
  Binary $$y$$ variables for discrete choices.
- **Parameters.** Composition $$a_{s,c}$$ (share of component $$c$$ in source $$s$$); extraction
  efficiency $$e_{p,c}$$; supply available per source; capacity per plant; quota per
  component; margin per unit of each product; processing cost.
- **Production.**

  $$
  \text{out}_c = \sum_s \sum_p a_{s,c}\, e_{p,c}\, x_{s,p}
  $$

  Linear in $$x$$ because composition and efficiency are given numbers.
- **Constraints.**

  $$
  \begin{aligned}
  \sum_p x_{s,p} &\le \text{supply}_s && \text{for each source} \\
  \sum_s x_{s,p} &\le \text{capacity}_p && \text{for each plant} \\
  \text{out}_c &\ge \text{quota}_c && \text{for each component} \\
  x_{s,p} &\le M\, y_{s,p} && \text{links flow to an on-off decision, if any}
  \end{aligned}
  $$

- **Objective.** Maximise $$\sum_c \text{margin}_c \cdot \text{out}_c - \text{costs}$$.
- **Where integers come from (typical).** A plant or line being on or off; a minimum
  throughput if a plant runs at all; a limited number of source switches; discrete
  operating modes.
- **Why optimisation and not a rule.** The sources differ in richness and the plants in
  efficiency per component, so the best pairing depends on quotas and prices together;
  planners cannot enumerate it by hand.
- **Outputs the planner needs.** The allocation table, production against quota, margin,
  and which constraints are binding.

## On my CV

"Scoped and built a mixed-integer optimizer (PuLP, CBC) for weekly planning that allocates
natural gas from three sources of differing composition across four processing plants,
meeting each component's quota at the highest margin."

**To fill in (only I know):**

- Which decisions were integer or binary, and why.
- Whether efficiency was fixed per plant or depended on the feed (if it depended on the
  blend, how that was kept linear).
- Model size and solve time.
- How scoping went: who the users were, what they did before, how the plan was validated.
- Any outcome (margin, planning time), if I can state one.

## Likely questions

1. **Walk me through the formulation.** Sets, variables, constraints, objective, in that
   order, as above.
2. **Why is it mixed-integer and not linear?** Name the actual discrete decisions.
3. **What if the quotas cannot all be met?** The model is infeasible; add slack variables
   with penalties so it returns the least-bad plan and shows which quota is short.
4. **How did you validate it?** Reproduce past weeks, compare with the planners' actual
   plans, and review cases where it disagrees with them.
5. **Senior follow-up: how did you scope it with the client?** From their planning
   process: decisions, constraints they respect in practice (often unwritten), data
   available, and the planning horizon.

## Pitfalls

- Describing it as "AI" rather than an exact optimisation with a provable gap.
- Forgetting unwritten operating constraints until the planners reject the plan.

## Sources

- Williams, *Model Building in Mathematical Programming* (blending and refinery examples): <https://www.wiley.com/en-us/Model+Building+in+Mathematical+Programming%2C+5th+Edition-p-9781118443330>
- PuLP, a blending problem case study: <https://coin-or.github.io/pulp/CaseStudies/a_blending_problem.html>
- Natural-gas processing: <https://en.wikipedia.org/wiki/Natural-gas_processing>
