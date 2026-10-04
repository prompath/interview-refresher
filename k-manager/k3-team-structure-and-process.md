[Contents](../index.md) · K3 · Manager extras

# Team structure and process

## In one minute

How a data science team is organised decides whom it listens to and how its work reaches
production. Central teams keep standards and careers strong but drift from the business;
embedded scientists are close to decisions but isolated. Most organisations settle on a
hybrid. Process should fit the work: agile rhythms help, provided research uncertainty is
handled with time-boxes rather than forced into fixed-size tickets.

## Key ideas

- **Structures.**
  - *Centralised*: one team serving all units. Consistent methods, shared tooling, clear
    careers; risk of becoming a ticket queue far from the business.
  - *Embedded (decentralised)*: scientists sit in business units. Context and speed;
    risk of duplicated work, uneven standards, lonely careers.
  - *Hybrid or hub-and-spoke*: scientists embedded in units, reporting to or supported by
    a central function for standards, tooling and career growth.
- **Roles.**
  - *Data analyst*: reporting, exploration, business questions.
  - *Data scientist*: modelling, experimentation, causal questions.
  - *Machine learning engineer*: production pipelines, serving, CI/CD.
  - *Data engineer*: ingestion, data models, platform.
  - *Product or business owner*: priorities and adoption.
  Small teams need people who span roles; larger teams specialise.
- **Ratios and gaps.** A team of scientists with no engineering support ships notebooks;
  the commonest structural problem.
- **Agile for data science.**
  - Works: short cycles, visible backlog, regular demos, retrospectives, stakeholder
    contact.
  - Fits badly: estimating research in story points; "done" for an experiment whose
    answer is unknown.
  - Adaptation: time-boxed spikes with a question and a decision at the end; kanban for
    maintenance and ad-hoc requests; definition of done includes measurement.
- **Rituals worth having.** Planning, short stand-ups, a weekly technical review of
  methods and results, retrospectives.
- **Intake.** One route for requests, triaged by value and effort, so the team is not
  driven by whoever asks loudest.
- **Maintenance load.** Every production model takes ongoing time; budget it explicitly.
- **Shared assets.** Project template, standards, feature definitions, an experiment
  log.
- **On-call and ownership.** Each pipeline has a named owner and a runbook.

## My evidence

I have worked in three settings: a research institute and its spin-off, a consultancy
with client projects, and an in-house team with scrum, vendors and a business team. I can
compare them from experience.

## Likely questions

1. **Central or embedded?** Trade-offs, and hybrid as the usual answer; depends on size
   and maturity.
2. **Does scrum work for data science?** Partly; say what I would keep and change.
3. **How do you split work between scientists and engineers?** By outcome ownership with
   shared standards, pairing at the handover to production.
4. **How do you handle ad-hoc requests?** A triage route and a capacity reserve.
5. **What would you change in the first 90 days?** Listen first: map the work, owners
   and pain points, then fix one visible problem.

## Sources

- Sigma, "The Data Org Dilemma: What Structure Actually Scales": <https://www.sigmacomputing.com/blog/data-org-dilemma>
- Postman, "How It Works: The Postman Data Team's Hub-and-Spoke Model": <https://blog.postman.com/how-postman-data-team-uses-hub-and-spoke-model/>
- Fournier, *The Manager's Path* (2017): <https://www.oreilly.com/library/view/the-managers-path/9781491973882/>
- Data Science Process Alliance, agile for data science: <https://www.datascience-pm.com/agile-data-science/>
