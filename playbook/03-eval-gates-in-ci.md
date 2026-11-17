# 3 · Eval Gates in CI

Unit tests answer "does the code do what the code says?" Evals answer the question agentic systems add: **"does the behavior still meet the bar?"** — where behavior is non-deterministic, "correct" has gradations, and the grader may itself be a model. If changes to prompts, models, tools, or agent logic can reach production without an eval gate, you are shipping on vibes with extra steps.

## The minimum viable machinery

Four components, adoptable in this order (reference implementation: [evalgate](https://github.com/vmagapu/evalgate)):

1. **A case suite that represents reality.** Golden scenarios from real (sanitized) traffic, tagged by capability. Start embarrassingly small — 50 honest cases beat 5,000 synthetic ones — and grow it from every incident: *each production failure becomes a case before the fix merges*, which is how the suite converges on your actual risk surface.
2. **Judges — deterministic where possible, calibrated where not.** Exact/contains/numeric checks cover more than teams expect. Where judgment is required, an LLM judge is a measurement instrument and must be measured: validated against human-labeled examples, reported with chance-corrected agreement (kappa), and re-calibrated whenever the judge's model or prompt changes. An uncalibrated judge is a random-number generator with gravitas.
3. **A committed baseline.** Scores from the last accepted run, in the repo, next to the code they measure. The diff *is* the review artifact.
4. **The gate.** Fails the build on: mean-score drops beyond tolerance, **per-tag drops** (regressions hide inside healthy aggregates), and any case flipping pass→fail — the failure mode where a change fixes ten cases, breaks ten others, and the mean stays flat.

A working GitHub Actions workflow is in [`examples/ci/eval-gate.yml`](../examples/ci/eval-gate.yml).

## Rules that keep the gate honest

- **The gate binds by tier.** T2+ changes touching model behavior cannot merge red. T0/T1 run evals as signal, not blockage — a gate that blocks everything teaches people to route around it.
- **A red gate stops the ship. Actually.** The first time leadership overrides a red gate for a date, the gate becomes advisory forever. Overrides exist, but they are risk acceptances: named owner, written rationale, expiry date, visible to everyone.
- **Flaky evals are fixed with the same urgency as flaky tests.** Non-determinism in the *grader* (temperature, unseeded sampling, judge drift) destroys trust fastest of all. Seed everything seedable; quantify variance for the rest and set thresholds above the noise floor.
- **Judge-shopping is a defect.** Rerunning until green, switching judges mid-stream, or trimming embarrassing cases are the eval-era equivalents of deleting failing tests. Make baseline and case-suite changes reviewable events with their own required approver.
- **Cost is part of the gate's budget.** Evals on every commit can out-spend the feature. Tier the suites: smoke evals per commit, full suites pre-merge for gated tiers, exhaustive suites nightly. Meter the spend like any other model spend (ch. 4).

## What "good" looks like after a quarter

Engineers add eval cases the way they add tests — unprompted, because it protects them. The baseline diff appears in PR review alongside the code diff. Incidents produce cases within a day. And the question "how do we know the new model/prompt is safe to ship?" has a boring, procedural answer — which is the entire point. Boring is what trust feels like from the inside.
