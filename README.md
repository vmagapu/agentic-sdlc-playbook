# The Agentic SDLC Playbook

**How to move an engineering organization from AI-assisted coding to agentic delivery — with human judgment at the gates, and the results measured.**

This is not a thought piece. I ran this transformation across a 150+ engineer organization at Japan's largest consumer marketplace — evaluation gates in CI, governance guardrails, a versioned prompt library, an owned and metered LLM budget — producing a **measured ~40% developer-productivity improvement, instrumented through DORA metrics and sustained through enablement rather than mandate**. I also run the solo version daily as founder of an AI-native product, building with coding agents on top of my own [MCP server](https://github.com/vmagapu/finance-engines-mcp), [eval harness](https://github.com/vmagapu/evalgate), and [LLM gateway](https://github.com/vmagapu/modelgate). This playbook is what survived contact with both scales.

## The one-paragraph thesis

Agents change *who types*, not *who is accountable*. The organizations that win this transition redesign the SDLC so agents do more of the work while humans own judgment at explicit gates — product intent, architecture, and risk acceptance — and they prove the change with operational metrics against a baseline, not with enthusiasm surveys. Adoption is won by making the new way visibly better, never by mandate: a mandate gets you compliance theater; enablement gets you a curve that keeps rising after you stop pushing.

## The playbook

| Chapter | Question it answers |
|---|---|
| [1 · Operating model](playbook/01-operating-model.md) | What changes in the SDLC, and what must never change |
| [2 · Risk tiers](playbook/02-risk-tiers.md) | How much autonomy an agent gets, decided *before* the work |
| [3 · Eval gates in CI](playbook/03-eval-gates-in-ci.md) | How non-deterministic changes earn the right to ship |
| [4 · Governance & cost](playbook/04-governance-and-cost.md) | Who decides, what's versioned, and who pays |
| [5 · Adoption](playbook/05-adoption.md) | Lighthouse teams → playbook → scale, without mandates |
| [6 · Measurement](playbook/06-measurement.md) | Proving it worked — and not fooling yourself |

Plus working artifacts: a [CI eval-gate workflow](examples/ci/eval-gate.yml) you can adapt today, and an [agent-change checklist](templates/agent-change-checklist.md) for reviewers.

## Who this is for

Engineering leaders (Director → CTO) accountable for making this transition real in organizations of 50–500+ engineers — especially in regulated or high-trust domains, where "the agent wrote it" will never be an acceptable answer to an auditor. Everything here assumes you must keep shipping while you transform: no pause, no rewrite, no pilot purgatory.

## Principles the whole playbook reduces to

1. **Humans own judgment; agents own toil.** The gates are product intent, architecture, and risk acceptance. Everything else is negotiable.
2. **Autonomy is earned per risk tier, not granted per team.** Decided before work starts, enforced in tooling, revisited on evidence.
3. **Evals are the new tests.** A change touching model behavior ships only through calibrated, regression-gated evaluation — in CI, not in a notebook.
4. **Govern with mechanisms, not memos.** Versioned prompts, metered budgets, audit trails, least-privilege tool access — policy as code, evidence automated.
5. **Measure operationally, at team level, against a baseline.** DORA plus AI-specific metrics; never individual surveillance, never self-reported enthusiasm.
6. **Enablement over mandate.** Champions, office hours, visible wins. The playbook spreads because teams want what the lighthouse teams have.

— [Vish Magapu](https://vmagapu.github.io) · Text CC BY 4.0, examples MIT
