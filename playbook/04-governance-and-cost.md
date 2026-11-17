# 4 · Governance & Cost: Mechanisms, Not Memos

Governance that lives in policy documents is governance that doesn't exist. Everything in this chapter is a *mechanism* — something versioned, metered, logged, or enforced in tooling — because that is the only form of governance that survives a deadline. I ran this as a standing structure with the CTO, CISO, and Legal in the room monthly; the meeting worked because every agenda item was backed by a mechanism, not a slide.

## The five mechanisms

**1. A versioned prompt & skill library.** Prompts, agent instructions, and shared skills are code: in a repo, owned, reviewed, versioned, and — where they matter — A/B tested before replacing the incumbent. The anti-pattern is prompt folklore: critical instructions living in one engineer's snippets file, invisible to review and impossible to roll back. If a prompt change can alter production behavior, it travels through the same tiered pipeline as code (ch. 2).

**2. Least-privilege tool access.** An agent's capabilities are an attack-and-blast-radius surface. Approved tool/MCP catalogs per tier; credentials scoped to the task, never the engineer's own; secured paths (money movement, PII, authz) require tools that *do not exist* in lower-tier agent configurations. The strongest guardrail is the capability the agent simply does not have.

**3. The immutable audit trail.** For every agent-assisted change of consequence: what was asked, what the agent proposed, what the human changed, who approved. Append-only, queryable, boring. This is what converts "can we prove it?" from a scramble into a lookup — and in regulated environments it is the difference between an interesting conversation with your auditor and a finding.

**4. An owned, metered budget.** Model spend gets an owner, per-call metering, and tags that map to teams and features — so the monthly conversation is "support-bot costs $X per resolved ticket and trending down," never "why is the API bill $400k?" Caps enforce *before* the call on runaway paths. Showback first (visibility changes behavior on its own); chargeback when the organization is ready to argue about it. Reference implementation of the metering layer: [modelgate](https://github.com/vmagapu/modelgate).

**5. A standing decision forum.** Monthly, one hour, decision-makers only — engineering, security, legal, finance. Standing agenda: tier-movement requests with evidence; new tool/model approvals; audit-trail exceptions; the spend report; incidents involving agents. The forum's product is *decisions recorded with owners* — if it produces observations instead, kill it and start over.

## Security posture, condensed

Treat the agent supply chain like the software supply chain, because it is one: approved model and tool registries with the same rigor as package registries; prompt-injection treated as an input-validation class (untrusted content never becomes instructions on secured paths); agent-reachable data classified exactly as human-reachable data — an agent with production access *is* production access. Target: **zero data leakage** as a standing, measured objective, not an aspiration. The mechanisms above make it auditable; the tier system (ch. 2) makes it enforceable.

## The sequencing mistake to avoid

Teams instinctively govern first and enable second — a committee before a single lighthouse team has shipped. Invert it: stand up mechanisms 1–4 *with* the first lighthouse teams (ch. 5), let real usage surface the real risks, then convene the forum to govern evidence rather than hypotheticals. Governance designed before contact with reality optimizes for imagined failure modes and strangles the actual work.
