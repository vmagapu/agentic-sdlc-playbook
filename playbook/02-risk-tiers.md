# 2 · Risk Tiers: Autonomy Is Earned, Not Granted

The central governance question of agentic engineering is not "do we allow agents?" It is: **for this class of change, how much autonomy does an agent get, and which human gate is mandatory?** Decide that *before* work starts, per change class — not per team, not per tool, and never in the heat of a deadline.

## A tier model that has survived contact

| Tier | Change class (examples) | Agent autonomy | Mandatory human gate |
|---|---|---|---|
| **T0 — Trivial** | Formatting, comments, test scaffolding, doc updates | Agent authors and merges behind green CI | None beyond CI (sampled audit) |
| **T1 — Routine** | Bug fixes with reproducing tests, internal refactors, config within bounds | Agent authors; auto-review assists | One human approval, lightweight |
| **T2 — Significant** | New features, API changes, schema migrations, dependency upgrades | Agent authors from an approved spec | Full review by a code owner **+ eval gate** |
| **T3 — Critical** | Anything touching money movement, authn/authz, PII, regulatory logic, or model behavior in production | Agent drafts only; may not self-iterate on secured paths | Named senior reviewer + risk sign-off + eval gate; audit trail mandatory |

Three design rules make the table real rather than decorative:

1. **Tiering is determined by what the change touches, not by what the author intends.** Enforce it mechanically where possible: path-based rules (a diff touching `payments/` is T3 no matter what the PR description says), schema-change detection, dependency manifests. Intent-based tiering is self-tiering, and self-tiering drifts down.
2. **The tier decides the pipeline, automatically.** T0 routes to the fast lane; T3 routes to the gated lane with required reviewers and mandatory evals. If routing requires a human to remember the policy, the policy will be forgotten on the worst possible day.
3. **Tiers move on evidence, in both directions.** A change class earns a lighter tier after a defined volume of clean history; it loses one after an incident. Publish the movement criteria — the legitimacy of the whole system rests on tiers being earned, not negotiated.

## The dangerous middle

T0 and T3 are easy to get right because they're obvious. The failure mode lives in T1/T2: changes that look routine but carry hidden blast radius — the "simple" dependency bump, the "mechanical" refactor across a domain boundary. Two mitigations: make blast-radius signals part of mechanical tiering (files touched, services affected, public-interface changes), and let any reviewer *escalate* a tier with one click, no justification required. Escalation must be free; de-escalation must be earned.

## Regulated environments

If you operate under PCI, banking, or health regimes, map tiers to your existing change-control classes rather than inventing a parallel system — auditors accept a familiar structure with a new author faster than a novel one. Two additions matter to them: an **immutable record of what the agent proposed vs. what a human changed**, and **separation of duties** (the person who prompted the change is not the person who approves T3). Both are cheap to automate on day one and impossible to retrofit after an audit finding.
