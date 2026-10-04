[Contents](../index.md) · B5 · P2

# Contextual bandits

## In one minute

A bandit chooses among actions (offers), sees the reward only for the one it chose, and
must balance exploiting what looks best with exploring what might be better. A contextual
bandit uses customer features to make that choice per customer. LinUCB assumes reward is
linear in the features and picks the arm with the highest optimistic estimate: predicted
reward plus an uncertainty bonus.

## Key ideas

- **Explore versus exploit.** Only the chosen arm's reward is observed, so a purely greedy
  policy can lock onto a mediocre arm.
- **Policies.**
  - *Epsilon-greedy*: random arm with probability ε, best arm otherwise.
  - *UCB*: choose the arm with the highest upper confidence bound; uncertainty shrinks as
    an arm is tried.
  - *Thompson sampling*: sample each arm's reward from its posterior and pick the best.
- **LinUCB (disjoint).** Per arm `a`, a ridge regression on context `x`:

  ```
  A_a = I + Σ x xᵀ          b_a = Σ r x          θ_a = A_a⁻¹ b_a
  score_a = θ_aᵀ x + α · sqrt( xᵀ A_a⁻¹ x )
  ```

  The first term exploits, the second explores; α sets how much.
- **Incremental updates.** `A_a` and `b_a` are sums, so each day's feedback is added
  without retraining from scratch (partial fit).
- **Arm exclusion.** Some arms are not allowed for some customers (already owned,
  incompatible promotion). Mask them at decision time.
- **Reward design.** Binary acceptance or revenue; delay between offer and reward means
  updates lag.
- **Regret.** Reward lost against the best policy in hindsight; good algorithms have
  regret growing sub-linearly.
- **Off-policy evaluation.** Estimate a new policy from logs with inverse propensity
  weighting; needs the logged probability of each choice. A random-policy group makes
  this easy.
- **Library.** MABWiser offers these policies behind one fit, partial-fit and predict
  interface.

## On my CV

"Maintained production upsell models: recommenders and a bandit for offer selection." I
maintain it: fixed an exclusion-logic bug that re-offered packages customers already held,
fixed an inference failure on single-row batches, and keep the exclusion mapping current.
I did not develop the model, and "bandits" is deliberately not in my Skills.

## Likely questions

1. **Why a bandit instead of a classifier?** It keeps learning from its own decisions and
   explores new or changed offers without a separate test.
2. **Explain the UCB term.** Uncertainty in the estimate for this context; large for
   contexts or arms seldom seen, so they get tried.
3. **How do you choose α?** Trade-off between exploration cost and adaptation speed;
   tuned offline on logged data or by an online comparison.
4. **How did you find the exclusion bug?** Customers were offered what they held; traced
   to "allowed if any promotion permits" where the rule should be "blocked if any
   promotion forbids".
5. **Senior follow-up: how do you know the bandit is working?** Compare with the random
   group and a static model on revenue per customer; watch arm distribution for collapse.

## Pitfalls

- Claiming to have built it.
- Calling it reinforcement learning without the distinction in
  [B6](b6-bandit-vs-reinforcement-learning.md).

## Sources

- Li et al., "A Contextual-Bandit Approach to Personalized News Article Recommendation" (2010): <https://arxiv.org/abs/1003.0146>
- MABWiser: <https://github.com/fidelity/mabwiser>
- Multi-armed bandit: <https://en.wikipedia.org/wiki/Multi-armed_bandit>
