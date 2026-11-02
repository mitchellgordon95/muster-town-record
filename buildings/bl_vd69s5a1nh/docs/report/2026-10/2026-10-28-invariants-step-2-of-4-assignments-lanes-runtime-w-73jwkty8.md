---
id: "dc_0b73jwkty8"
type: "report"
state: "building"
title: "Invariants step 2 of 4 (assignments & lanes, runtime & wakes): draft PR #63, commit 99deb96"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 2 done as specified (2 docs, 2 tests, AGENTS.md + architecture.md links, check:docs accepts test( as well as it(). I take the PR #63 review and merge myself. Step 3 (bank) starts from your queue."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T00:39:37.046Z"
sessionId: "se_g612oadi0i"
assignmentId: "as_lk59wvkpfc"
costUsd: 1.0763565000000002
tokens: 53818
turns: 28
createdAt: "2026-10-28T00:39:28.989Z"
updatedAt: "2026-10-28T00:39:37.046Z"
---
## What I did
I pulled main (PR #62 is merged) and added 2 tests, then wrote `docs/invariants/assignments-lanes.md` and `docs/invariants/runtime-wakes.md`. Both are linked from AGENTS.md (next to grants.md) and from the matching rows in docs/architecture.md. I also made one small extension to check:docs. Everything is in draft PR #63 (https://github.com/mitchellgordon95/muster-town/pull/63), head commit 99deb96. I didn't redeploy because only docs and tests changed.

## Findings
- **assignments-lanes.md** has 8 invariants: every assignment has a lane, and directed work needs a human source; a grant lane refuses closed, rejected and draft grants; exploration can't name a key result that has a funded grant; a session copies its lane and grantId; the gate holds work and never cancels it (the allowance holds exploration, never directed work); directed work stops once a grant proposal names its key result; waitFor holds the start (24 h cancel, at most 3 parks); one owner and one queue order, with reassign and cancel rules. The doc ends with a "How it connects" section covering grants, the budget and the runtime.
- **runtime-wakes.md** has 8 invariants: only the scheduler starts work, and never past canStart; durable wakes use a unique wakeKey; the Waker cursor replays nothing twice; one rule per event; never more than maxRunning sessions; one session per assignment across restarts; every session ends in a report or a fallback; nobody is woken without a human origin (with a hop cap, a time cap, and no forged origin). It also has a "How it connects" section.
- **New tests**, both passing when run alone:
  - `packages/core/test/lanes.test.ts`: "a grant assignment can't name a closed, rejected or draft grant; proposed, funded and checkpoint ones are accepted (and the gate holds the unfunded)". The lanes file passes 22/22.
  - `packages/runtime/test/queue.test.ts`: "a tick never starts an assignment that canStart refuses: a lane-held one stays pending with its reason and starts once the gate opens". The queue file passes 3/3.
- **A check change I hadn't planned:** the runtime tests use `test(` rather than `it(`, and the citation check only looked for `it(`. `scripts/check-doc-refs.ts` now accepts either.
- **Checks:** `npm run check:docs` passes on all 3 invariants docs. I broke a citation on purpose and it failed as it should. Core and runtime both typecheck. I didn't run the full suite; CI will.
- The only change to grants.md is that one sentence now links to assignments-lanes.md.

## What I need from you
Merge PR #63 once its CI is green.
