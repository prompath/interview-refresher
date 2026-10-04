[Contents](../index.md) · A5 · P1

# Control group holdouts

## In one minute

A global control group is a small random share of customers held out of *all* campaigns
for a period. Comparing everyone else with them gives the combined incremental effect of
the whole marketing programme, which per-campaign tests and attribution models cannot
give. Campaign-level controls then measure each campaign inside the treated population.

## Key ideas

- **Why a global holdout.** Campaign controls still receive other campaigns, so summing
  campaign uplifts double counts and misses interactions. Attribution splits credit among
  touches but cannot say what would have happened with no touch at all.
- **Layers.** Global control (no marketing) → campaign or use-case control (no *this*
  campaign) → test buckets (variants). The layers must be mutually exclusive where needed
  and assigned independently otherwise.
- **Sizing.** Larger holdout = tighter estimate but more revenue forgone. Size it from the
  power calculation for the programme-level effect over the measurement window.
- **Duration and rotation.** A long-term holdout measures cumulative effects but the
  customers held out drift (they miss upgrades, may churn differently). Rotate or refresh
  on a schedule, and keep the assignment history.
- **Assignment.** Deterministic and reproducible: a hash of a stable customer key plus a
  salt, mapped to buckets. New customers get assigned by the same rule. Stratify by key
  segments (product line, value tier) so the holdout mirrors the base.
- **Contamination.** Held-out customers still getting contacted (a channel that does not
  check the list, a shared household). Measure the leak rate; analyse by assignment.
- **Enforcement.** The holdout is only real if every campaign system excludes it. That is
  an engineering and governance task as much as a statistical one.
- **Monitoring.** Group proportions, balance on pre-period metrics, churn out of the
  holdout, leak rate.

## On my CV

- "Implemented the global control group holdout for a vendor multi-touch attribution
  project and contributed to its design." A principal data scientist designed it; I took
  part in the design discussions and built it. Say exactly that.
- "Built a daily PySpark job, reusing the holdout's sampling design, that assigns customers
  to test buckets for a second vendor's uplift tests."

## Likely questions

1. **Why hold customers out when you have attribution?** Attribution redistributes
   observed conversions; only a holdout shows how many would have happened anyway.
2. **How big should it be?** As small as still detects the programme-level effect in the
   reporting period. State the trade-off in forgone revenue.
3. **How do you keep assignment stable day to day?** Persist assignments; only new
   customers are sampled, by a deterministic hash, and re-runs are idempotent.
4. **What breaks a holdout over time?** Leakage, differential churn, product changes that
   reach everyone, and people forgetting to exclude it.
5. **Senior follow-up: the business objects to withholding offers.** Frame it as the cost
   of knowing whether the spend works; propose a small share, rotation so no customer is
   excluded forever, and exemptions for service messages.

## Pitfalls

- Sampling the holdout from customers already targeted (not representative of the base).
- Re-sampling each period, which destroys long-term measurement.
- Claiming "designed" for the holdout. I implemented it and contributed to the design.

## Sources

- Zyabkina, "Measuring Incrementality with Universal (Global) Control Groups": <https://zyabkina.com/universal-control-groups-and-advanced-experiments-in-marketing/>
- Bluecore Engineering, "Using Holdout Groups to Quantify Marketing Campaign Lift": <https://medium.com/bluecore-engineering/using-holdout-groups-to-quantify-marketing-campaign-lift-87e6883e3eab>
- Kohavi, Tang, Xu, *Trustworthy Online Controlled Experiments*, long-term effects and holdbacks: <https://experimentguide.com/>
