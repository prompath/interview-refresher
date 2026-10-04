[Contents](../index.md) · A3 · P1

# Multi-arm tests

## In one minute

A test with several arms answers several questions at once, so the chance of at least one
false positive grows with the number of comparisons. I decide beforehand which comparisons
matter (usually each treatment against control), size each arm for those comparisons, and
correct the significance level for the number of them.

## Key ideas

- **Family-wise error.** With `m` independent comparisons at α = 0.05, the chance of at
  least one false positive is `1 − 0.95^m`: 14% for three, 26% for six.
- **How many comparisons.** Four arms give three comparisons against a control, or six if
  every pair is compared. Fewer planned comparisons means less correction.
- **Corrections.**
  - *Bonferroni*: test each at α/m. Simple, conservative.
  - *Holm*: sort p-values, compare the smallest with α/m, the next with α/(m−1), and so on;
    stop at the first failure. Never worse than Bonferroni.
  - *Dunnett*: built for many treatments against one control.
  - *Benjamini-Hochberg*: controls the false discovery rate rather than any false
    positive; suited to many exploratory comparisons.
- **Omnibus first.** A chi-square test across all arms asks "is any arm different?".
  Useful as a gate, but it does not say which arm.
- **Sample size.** Size each arm for the pairwise comparison at the corrected α. When
  every treatment is compared with one control, giving the control more than an equal
  share (about √k times a treatment arm for k treatments) improves power.
- **Picking the winner.** The best-looking arm is biased upward (winner's curse). Confirm
  the chosen arm against control in a follow-up or with a holdout.
- **Factorial designs.** If arms are combinations of two factors (2×2), main effects and
  the interaction can be estimated from the same sample.

## On my CV

"A four-arm right-time-to-call test." Be ready to state the arms, which comparisons were
planned, and how the multiple comparisons were handled. See
[A11](a11-right-time-to-call.md).

## Likely questions

1. **Why not run three separate A/B tests?** One shared control uses fewer customers and
   all arms run in the same period, so they are comparable.
2. **Bonferroni or Benjamini-Hochberg?** Bonferroni or Holm when a single false win is
   costly and comparisons are few; Benjamini-Hochberg when screening many.
3. **Two treatment arms both beat control but do not differ from each other. Which do you
   ship?** The cheaper or simpler one; the test does not support a preference.
4. **How does adding an arm change the duration?** Each arm needs its own n, and the
   correction raises n per arm, so total traffic grows faster than linearly.
5. **Senior follow-up: when would you use a bandit instead?** When the goal is to earn
   during the test rather than to learn a clean effect size, and arms are many or
   short-lived. See [A10](a10-testing-adaptive-model.md).

## Pitfalls

- Comparing all pairs after the fact and reporting the significant ones.
- Splitting equally by habit when all comparisons share one control.
- Reading the winning arm's observed effect as its true effect.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*, multiple testing: <https://experimentguide.com/>
- Multiple comparisons problem: <https://en.wikipedia.org/wiki/Multiple_comparisons_problem>
- Holm-Bonferroni method: <https://en.wikipedia.org/wiki/Holm%E2%80%93Bonferroni_method>
- False discovery rate: <https://en.wikipedia.org/wiki/False_discovery_rate>
