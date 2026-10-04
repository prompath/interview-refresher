[Contents](../index.md) · B6 · P2

# Bandit versus reinforcement learning

## In one minute

A bandit makes one-step decisions: choose an action, get a reward, and the next customer
is unaffected. Full reinforcement learning handles sequences: an action changes the state,
rewards can arrive later, and the agent optimises the long-run total. A contextual bandit
is reinforcement learning with a horizon of one. Many systems called "RL" in marketing are
contextual bandits.

## Key ideas

- **The ladder.**
  - *Multi-armed bandit*: actions and rewards, no context.
  - *Contextual bandit*: context → action → immediate reward.
  - *Reinforcement learning*: state → action → reward and next state; maximise discounted
    return $$\sum_t \gamma^t r_t$$.
- **Markov decision process.** States, actions, transition probabilities, rewards,
  discount $$\gamma$$. A *policy* maps states to actions; a *value function* gives expected return.
- **Core RL ideas by name.** Q-learning (learn action values with the Bellman update),
  policy gradient (optimise the policy directly), temporal difference learning, credit
  assignment for delayed reward.
- **When a bandit is enough.** The offer's effect is seen quickly and does not much change
  what should be offered next.
- **When full RL is warranted.** Sequences matter: a cheap offer now changes willingness
  to upgrade later; contact fatigue; a multi-step journey (next best action over months).
- **Why full RL is hard in marketing.** Sparse and delayed rewards, little data per
  customer, no simulator, and exploration that costs real revenue. Off-policy learning
  from logs is fragile.
- **Next best action.** Choosing among offers, channels and timings per customer. Usually
  built as propensity models per action plus rules or a bandit, rarely as full RL.

## On my CV

The CV says "a reinforcement learning offer model" because that is what the model is
called at work. If asked, be precise: it is a contextual bandit, updated daily, which is
the one-step case of reinforcement learning.

## Likely questions

1. **Is a contextual bandit reinforcement learning?** It is the special case with no
   state transitions and immediate reward.
2. **Give an example where a bandit would fail.** When this month's discount lowers next
   month's acceptance of a full-price upgrade; the bandit optimises each offer alone.
3. **What would you need to move to full RL?** A state definition, long-horizon reward
   (lifetime value), enough logged trajectories, and a safe way to explore.
4. **What is the Bellman equation saying?** The value of a state is the immediate reward
   plus the discounted value of the next state.
5. **Senior follow-up: would you recommend full RL for next best action?** Not first.
   Start with a bandit and a long-horizon reward proxy; move only if sequence effects are
   shown to matter.

## Pitfalls

- Using "RL" loosely with an interviewer who knows the difference.
- Ignoring delayed reward when the conversion window is a billing cycle.

## Sources

- Sutton and Barto, *Reinforcement Learning: An Introduction* (2nd ed.): <http://incompleteideas.net/book/the-book-2nd.html>
- Li et al., LinUCB paper (2010): <https://arxiv.org/abs/1003.0146>
- Markov decision process: <https://en.wikipedia.org/wiki/Markov_decision_process>
