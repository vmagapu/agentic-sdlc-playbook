# 1 · The Operating Model

## What actually changes

The traditional SDLC assumes the expensive resource is typing. Agents invert that: generation becomes cheap, and the scarce resources become **intent** (knowing precisely what to build), **judgment** (knowing whether what was built is right), and **context** (the institutional knowledge that makes both possible). The operating model reorganizes around those three.

Stage by stage:

| Stage | Before | Agentic |
|---|---|---|
| Requirements | Prose tickets, intent in people's heads | Specs and acceptance criteria written to be executable — they are now *source code for agents* |
| Design | Docs reviewed by humans | Unchanged in authority, richer in input: agents draft options; a human architect decides and signs |
| Build | Engineers type; review catches defects | Engineers orchestrate one or more agents; review shifts from "is this code right" to "is this *change* right" |
| Test | Humans write tests after | Agents generate tests with the change; eval suites cover behavior tests can't reach (ch. 3) |
| Release | CI gates on tests | CI gates on tests **and evals**, routed by risk tier (ch. 2) |
| Operate | On-call reads dashboards | Same accountability; agents draft incident analysis, humans own the postmortem's conclusions |

## What must never change

Three gates stay human, permanently, and I recommend writing them into your engineering constitution so nobody relitigates them per-project:

1. **Product intent** — what we are building and why. An agent amplifies intent; it must not originate it.
2. **Architecture** — the decisions that are expensive to reverse. Agents propose; a named human architect disposes.
3. **Risk acceptance** — shipping anything with regulatory, financial, security, or customer-trust consequence. "The agent was confident" is not a risk acceptance.

Accountability is the invariant. When an agent-authored change breaks production, the question in the postmortem is the same as it ever was: which *human* accepted this risk, and what did they know? If your operating model can't answer that, you don't have an agentic SDLC — you have deniability engineering.

## The role shift, said plainly

- **Engineers** move from writing most code to specifying, orchestrating, and verifying it — one engineer running multiple agent workstreams in parallel is the steady state, and it is a *harder* job, not an easier one. The skill ceiling goes up.
- **Senior engineers and architects** become the highest-leverage people in the building: their judgment is now applied across far more change volume. Protect their time for exactly that.
- **Managers** stop proxying status (agents and dashboards do that) and concentrate on the two things that got scarcer: growing judgment in their people, and making priority calls.

A word of caution from running this at scale: do not rebrand job titles on day one. Change the work, measure the result, and let the role definitions follow the reality — titles changed by memo produce cynicism; titles changed by evidence produce careers.

## The spec is the new bottleneck

The single highest-ROI practice change: treat specifications and acceptance criteria as first-class, versioned artifacts, written precisely enough that an agent can act on them and an eval can verify them. Vague tickets were survivable when a human filled the gaps from context; an agent fills them from plausibility. Teams that invest in spec quality compound; teams that don't generate rework at machine speed.
