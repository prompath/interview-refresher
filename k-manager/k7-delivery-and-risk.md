[Contents](../index.md) · K7 · Manager extras

# Delivery and risk

## In one minute

A manager is accountable for delivery and for what happens when things go wrong. I track
projects by risk rather than by percentage complete, surface slips as soon as they are
likely, run incidents calmly with a blameless review afterwards, and treat personal data
protection and model governance as part of the work, since a telecom or bank holds data
that the law protects.

## Key ideas

- **Tracking.** Milestones with decision gates; the top risks and their owners; early
  warning signs (data not arriving, a baseline not beaten).
- **A slipping project.** Find the cause (scope, data, dependency, capacity); present
  options: cut scope, move the date, add help, or stop; decide with the stakeholder;
  tell everyone affected early.
- **A failed project.** Many data science projects do not reach production. Limit the
  loss with gates; record what was learned; do not hide it.
- **Production incidents.**
  1. Contain: stop or roll back the bad output.
  2. Communicate: who is affected, what we know, when the next update comes.
  3. Fix and verify.
  4. Blameless review: timeline, causes, what made it possible, actions with owners.
- **Prevention.** Monitoring, data checks that fail the job, runbooks, tested rollback,
  no single person who alone understands a pipeline.
- **Personal data (PDPA).** Thailand's Personal Data Protection Act B.E. 2562 (2019),
  in force since June 2022, is broadly modelled on the GDPR:
  - a lawful basis (consent, contract, legitimate interest and others);
  - purpose limitation and data minimisation;
  - data subject rights (access, correction, deletion, objection);
  - security measures and breach notification;
  - rules for transfers abroad and for processors (vendors).
  For a model: is this use covered by the purpose and basis, is the data needed, who
  has access, how long is it kept.
- **Model governance.** Inventory of models with owners; documentation of purpose, data,
  limits and performance; approval before deployment; periodic review; audit trail.
- **Fairness and harm.** Check outcomes across customer groups; avoid proxies for
  protected attributes where they would cause unfair treatment; a route for complaints.
- **Automated decisions.** Keep human review where decisions are significant for the
  person.
- **Language models.** Extra risks: data sent to third parties, hallucinated output,
  prompt injection.
- **Bus factor and continuity.** Documentation and shared ownership.

## My evidence

Maintaining production pipelines and fixing defects in them; a write guard on evidence
tables; deciding data handling with vendors; documenting models and rules so knowledge is
not held by one person.

## Likely questions

1. **A key project will miss its date. What do you do?** Cause, options, early
   communication.
2. **Tell me about a production incident.** A prepared story with the review.
3. **How do you make sure models comply with data protection law?** Purpose and basis
   check, minimisation, access control, vendor terms, documentation.
4. **How do you govern ten models with a small team?** Inventory, owners, tiered
   scrutiny by business exposure.
5. **How do you build a blameless culture?** By how I react to the first mistake someone
   reports.

## Sources

- Thailand Personal Data Protection Committee (PDPC): <https://www.pdpc.or.th/>
- Google SRE book, "Postmortem Culture: Learning from Failure": <https://sre.google/sre-book/postmortem-culture/>
- Mitchell et al., "Model Cards for Model Reporting" (2019): <https://arxiv.org/abs/1810.03993>
