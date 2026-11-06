---
id: "dc_0fr3jwfn91"
type: "report"
state: "building"
title: "Grant C step 1: PR #381 drops the checkpoint session and checkpoint_grant; grants now hold at grant − min(150k, a third). Parked on CI"
authorId: "ag_r84jts3ld0"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_nqgbjho18g"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/381"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Grant C step 1 as planned: PR #381 (draft) drops the checkpoint session + checkpoint_grant, hold at grant − min(150k, ⌊grant/3⌋), continue → 100% hold, adjust recomputes, no sweep, holdAtTokens on GET /api/grants/<id>. Continuation as_i2f4njuql6 waits on PR #381's CI and merges. Step 2 (submit_report keyResults/topUp evidence, evidence() + card/deck) goes on the queue now, waiting on that continuation."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T22:56:57.470Z"
sessionId: "se_d1myo1bprf"
assignmentId: "as_xg977jopw3"
costUsd: 2.5593944999999994
tokens: 127970
turns: 48
createdAt: "2026-11-05T22:56:35.974Z"
updatedAt: "2026-11-05T22:56:57.470Z"
---
## What I did
I rebased on main after grant B step 1 (1bbaf18) and built step 1 of grant gr_95svkzi4l6. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/381. CI is still running, so I parked on it. The continuation merges the PR if CI is green.

## Findings
**What was removed.** Nothing replaces any of these: there is no fallback.
- The manager's "Write the checkpoint" assignment. The code that created it, the code that cancelled it, and `fileCheckpoint` are deleted.
- The `checkpoint_grant` tool: its verb, schema, describe line and prompt text.
- The lane-gate exception that let the checkpoint assignment run during a hold. A held grant now holds every new session on it.
- The ops.ts retry special case.
- The checkpoint-rollup link in submit_report. The close_grant link stays.

**The new hold rule.**
- A funded grant holds when its spend reaches its tokens minus a reserve. The reserve is min(150k, ⌊tokens/3⌋), computed and never stored.
- After a human continues a held grant, it holds again at 100%. An adjust recomputes the hold point.
- `checkpointsDone` records which holds have fired: 0 is the reserve hold, 1 is the 100% hold.
- A grant already held when this lands stays held. A funded grant already past its hold point holds at its next charge. There is no migration and no sweep.
- The 50% repair (`releaseHalfway`) now frees only legacy 0.5 holds. Otherwise it would have released reserve holds every time the server boots.
- `GET /api/grants/<id>` returns `holdAtTokens`. The spend line on the grant row reads "… (52%) · holds at 1.5M".
- I did not change the Bank: its claims, earmarks and overdraft walk are as before.

**Tests.**
- New core tests cover: holds at 66,667 / 300k / 850k for grants of 100k / 450k / 1M; no assignment is created at a hold; held grants keep new work waiting; continue then holds at 100%; adjust gives a new hold point; a held grant is untouched; a grant already past its point holds at its next charge; the verb is gone.
- I rewrote the tests that used the deleted functions rather than skipping them: review-deck and server grants now set the evidence directly until step 2.
- Results: core 801/802 on the full run; the one failure was my own assertion, which counted grant B's step-1 rows. I fixed it and the 3 affected files re-ran green (45/45). Server 296/297 on the full run; the one failure was `backup.test.ts` timing out while the core suite ran alongside it, and it passed alone (31/31 with grants). Typecheck is clean, and the web keyResults test passes.

**Docs.** I updated how-work-gets-done, goal-directed-budgets, invariants/grants, architecture, waterfall and wakes, and added a line to docs/log.md.

**What a human checks once it is live.** The first grant that holds after this lands should show "holds at N" on its spend line before the hold. When it holds, no "Write the checkpoint for …" assignment appears. Spend should stay at or under the grant while it is held.

**Left out of step 1:** nothing from the plan. The evidence fields on submit_report, the evidence() changes and the card/deck are step 2, as the assignment said. The plan for steps 2–4 is on the topic page [dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md).

## What I need from you
Nothing needed.
