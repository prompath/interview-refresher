[Contents](../index.md) · J5 · P2

# Technical leadership

## In one minute

A lead without direct reports leads through the quality of the team's work: setting
standards people actually follow, reviewing code and analysis so others grow, breaking
ambiguous work into pieces others can own, and deciding when to pay down technical debt.
The measure is what the team delivers, not what I deliver myself.

## Key ideas

- **Code review.** Purpose: catch defects, share knowledge, keep the codebase consistent.
  Review for correctness and tests first, then design, then style (which a linter should
  handle). Comments specific and kind; say what is good; distinguish "must fix" from
  "suggestion". Small pull requests, reviewed quickly.
- **Reviewing analysis.** Is the question right, is the comparison fair, is the
  uncertainty stated, could I reproduce it?
- **Standards.** Few, written, with reasons, enforced by tooling where possible, and
  changed through discussion. A project template makes the right way the easy way.
- **Mentoring.** Give problems, not solutions; pair on the first one; review the plan
  before the work; let them present their own results.
- **Delegation.** State the outcome and constraints, not the steps; match the task to
  the person's stretch; check in early rather than rescue late.
- **Design decisions.** Write a short design note for anything costly to reverse:
  context, options, decision, consequences. Disagree in the review, commit after it.
- **Technical debt.** Make it visible (a list with risk and cost), fix it alongside
  related feature work, and refactor behind behaviour-preserving checks.
- **Raising the bar without blocking.** Require tests for changed code, not for the whole
  legacy at once.
- **Knowledge sharing.** Documentation of pipelines and business rules, short internal
  talks, onboarding guide.
- **Influence without authority.** Earned by being right about risks, by helping others
  ship, and by making trade-offs explicit for the manager to decide.
- **Senior versus lead.** Senior: owns ambiguous problems end to end. Lead: sets
  direction for several people's work and is accountable for the team's technical
  outcomes.

## My evidence

Wrote the Sertis coding standards; refactored inherited pipelines onto the team template
at AIS; documented models, pipelines and business rules; taught 200+ students; advised
vendors on models and data handling. I have not formally led a team: say so, and show the
leading I have done.

## Likely questions

1. **How do you review code?** The order above, with an example.
2. **Tell me about mentoring someone.** A prepared story (teaching assistant work
   counts).
3. **How do you introduce a standard to a team that has none?** Start from a real
   incident, propose the smallest rule that would have prevented it, automate it.
4. **When do you refactor?** When the debt slows or endangers current work, and with a
   check that behaviour is unchanged.
5. **Lead-level follow-up: two seniors disagree on an approach.** Get both options
   written down with trade-offs, decide by criteria agreed first, time-box, and record
   the decision.

## Pitfalls

- Claiming formal leadership I have not had.
- Describing leadership only as doing the hardest tasks myself.

## Sources

- Google Engineering Practices, code review guide: <https://google.github.io/eng-practices/review/>
- Larson, *Staff Engineer* (guides on technical leadership): <https://staffeng.com/guides/>
- Reilly, *The Staff Engineer's Path* (2022): <https://www.oreilly.com/library/view/the-staff-engineers/9781098118723/>
