[Contents](../index.md) · A11 · P2

# Right-time-to-call

## In one minute

Right-time-to-call asks whether *when* a customer is called changes the result. The
experiment randomises customers across timing strategies and compares contact rate and
conversion. With four arms, the analysis follows [multi-arm tests](a3-multi-arm-tests.md).

## Key ideas

- **Two outcomes in sequence.** Answer rate (did the customer pick up) and conversion
  given contact. Timing mostly moves the first. The business metric is conversion per
  *assigned* customer, which combines both.
- **Typical arms.** Business-as-usual timing; a model-predicted best slot; a random slot;
  a fixed rule (for example evenings). A random arm separates "the model helps" from "any
  change in timing helps".
- **Unit and assignment.** Customer-level randomisation before the calling list is built;
  the call centre must follow the assigned slot.
- **Capacity constraint.** Agents are limited. If one arm gets the best agents or the
  first calls of the day, arms interfere. Balance agents and attempts across arms.
- **Compliance.** Customers may not be called in their assigned slot. Analyse by
  assignment (intention to treat) and report the compliance rate.
- **Confounding to avoid.** Offer, script, list quality and number of attempts must be the
  same across arms, so that timing is the only difference.
- **Modelling the slot.** A classifier of pick-up probability per customer per time slot,
  from past call outcomes and usage patterns; choose the slot with the highest
  probability subject to capacity.

## On my CV

"Designed A/B experiments, including a four-arm right-time-to-call test."

**To fill in (only I know):**

- What were the four arms?
- Primary metric: answer rate, conversion, or both?
- Which comparisons were planned, and what correction was used?
- Sample size per arm and duration, in relative terms.
- The result and the decision taken from it.

## Likely questions

1. **Why four arms?** State each arm's purpose, in particular which arm is the control and
   which isolates the model's contribution.
2. **How did you make sure the call centre followed the design?** List generation per
   slot, monitoring of calls per arm per slot, compliance rate.
3. **Answer rate rose and conversion did not. Why?** Reached customers who were available
   but not interested; timing changes who answers, not what they want.
4. **How did you handle customers called more than once?** One assignment per customer;
   outcome defined over the campaign window, not per attempt.
5. **Senior follow-up: would you roll it out?** Depends on uplift against the operational
   cost of scheduling by slot; propose a staged rollout with a holdout.

## Pitfalls

- Measuring conversion only among answered calls.
- Arms sharing constrained agent capacity unevenly.

## Sources

- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments* (design, triggering, interference): <https://experimentguide.com/>
- Intention-to-treat analysis: <https://en.wikipedia.org/wiki/Intention-to-treat_analysis>
