# Reviewer checklist — agent-assisted change

*For T2+ changes (see playbook ch. 2). The review question is not "is this code plausible?" — agents are excellent at plausible. It is "is this **change** right?"*

**Intent**
- [ ] The change maps to a written spec / acceptance criteria — not just a prompt someone remembers
- [ ] Scope matches the spec: nothing extra "helpfully" added (agents over-deliver; over-delivery is unreviewed surface)

**Tier & routing**
- [ ] Tier assigned mechanically matches what the diff actually touches (check paths, schemas, public interfaces)
- [ ] If anything in the diff feels heavier than its tier — escalate. Escalation is free.

**Correctness beyond plausibility**
- [ ] Tests assert *behavior the spec requires*, not merely behavior the implementation exhibits (agent-generated tests love to enshrine the bug)
- [ ] Edge cases and error paths are handled, not narrated in comments
- [ ] No hallucinated interfaces: every API/library/config referenced actually exists at the pinned version

**Security & data**
- [ ] No new credentials, broadened permissions, or widened tool access smuggled in
- [ ] Untrusted input cannot become instructions on any path this change touches
- [ ] Nothing in the diff moves data across a classification boundary

**Evals (if model behavior is touched)**
- [ ] Eval suite ran; gate is green — or an override exists with named owner, rationale, and expiry
- [ ] Baseline changes in this PR are intentional and reviewed as such
- [ ] New failure mode discovered during review? It becomes a case in this PR.

**Accountability**
- [ ] Audit trail intact: prompt/task reference, agent output, human modifications
- [ ] I can explain this change in the postmortem without the word "apparently"

*Approving this PR means a human accepted this risk. That human is you.*
