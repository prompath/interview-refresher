[Contents](../index.md) · K4 · Manager extras

# Roadmap and prioritisation

## In one minute

A data science roadmap is a short list of outcomes the business cares about, each with an
owner, a measure and a next decision point, plus reserved capacity for maintenance and for
exploration. I prioritise by expected value against effort and risk, make the trade-offs
visible to stakeholders, and say no by showing what a yes would displace.

## Key ideas

- **Start from business goals.** Each item traces to a goal the organisation has already
  stated.
- **Scoring.**

  $$
  \text{priority} \approx \frac{\text{value} \times \text{probability of success}}{\text{effort}}
  $$

  Value from a rough sizing; probability from data readiness and precedent. RICE (reach,
  impact, confidence, effort) is the same idea. The numbers are rough; the ranking
  conversation is the point.
- **Portfolio.** A mix of:
  - *run*: keeping production models healthy;
  - *improve*: measurable gains on existing systems;
  - *new*: new use cases;
  - *explore*: time-boxed bets.
  Say the split out loud (for example 30/30/30/10) and defend it.
- **Dependencies.** Data, engineering and business readiness often decide the order more
  than value does.
- **Quick wins and foundations.** Early visible results buy the trust to invest in
  measurement and platform work that pays later.
- **Roadmap format.** Now, next, later; outcomes rather than model names; decision gates
  rather than fixed dates for uncertain work.
- **Saying no.** "Yes, and here is what moves out", or "not now, because X ranks higher
  by the criteria we agreed". Offer a smaller version.
- **Stakeholder alignment.** Criteria agreed with business leads; roadmap reviewed with
  them on a regular rhythm; changes explained.
- **Stopping work.** Kill criteria set at the start; ending a project that is not
  working is a success of the process.
- **Maintenance against new work.** Unmaintained models lose value quietly; show the
  cost of neglect with monitoring data.
- **Review.** Compare predicted with realised value each quarter to improve the next
  round of estimates.

## My evidence

At AIS I keep an idea pipeline from research through plan to pitch, alongside
maintaining several production models; so I already balance new work against
maintenance on a small scale.

## Likely questions

1. **How do you prioritise competing requests?** Criteria, sizing, visible ranking.
2. **How do you say no to a senior stakeholder?** Show the displacement; offer options.
3. **How much time for research or exploration?** A stated small share, time-boxed, with
   a readout.
4. **How do you plan under uncertainty?** Gates and ranges, not fixed dates.
5. **A project is failing halfway. What do you do?** Check against the kill criteria,
   decide openly, capture what was learned.

## Sources

- Intercom, "RICE: Simple prioritization for product managers": <https://www.intercom.com/blog/rice-simple-prioritization-for-product-managers/>
- Huyen, *Designing Machine Learning Systems* (2022), on business objectives for machine learning: <https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/>
