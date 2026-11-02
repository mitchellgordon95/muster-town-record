---
id: "dc_euo9bss83c"
type: "report"
state: "building"
title: "The 04:16Z \"no-op\" key result wakes were goal-tree moves the wake mislabelled; fixed both sides (PR #153, efbd78f, redeploy queued)"
authorId: "ag_gtzy3w7qpk"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. The 04:16Z wakes were real goal-tree moves (accepted Planner proposals gp_7wbgaoguyc, gp_7zawcyxnjn) that wakes.ts describe() mislabelled \"marked <status>\"; PR #153 (efbd78f) fixes the label and makes a same-status, no-note PATCH a true no-op. Live check queued on deploy efbd78f."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T04:26:13.395Z"
sessionId: "se_1z0mmjijp4"
assignmentId: "as_261xv94bi9"
costUsd: 0.8979668
tokens: 44898
turns: 20
createdAt: "2026-10-31T04:23:46.968Z"
updatedAt: "2026-10-31T04:26:13.395Z"
---
## What I did
I read the event log from 69760 to 69784 on the live server. Then I fixed the wake label and added the server-side no-op guard in one PR, with tests. I merged it and queued a redeploy.

## Findings
- **No UI sent a status PATCH. Neither event was a no-op.** Event 69772 (kr_hj8wwx0q0w) and event 69781 (kr_2qg0ayfs1j) were real moves. Each key result moved from goal ob_s7jsvvoe5p to gl_join when Mitchell accepted the Planner's move proposals gp_7wbgaoguyc (event 69773) and gp_7zawcyxnjn (event 69782) in 1:1 mt_n25udpflus. They came from `goals.ts moveKr`, whose event text is "Key result moved to …" and whose payload has `status === from` plus `goalId`/`fromGoalId`.
- **The bug was the in-tray label.** `wakes.ts describe()` only recognised moves between objectives (`objectiveId`). A move between goals fell through to "marked <status>", so the rows [dc_khmfeo8foe](2026-10-31-key-result-kr-hj8wwx0q0w-marked-not-started-by-mit-mfeo8foe.md) and [dc_57injqjvh1](2026-10-31-key-result-kr-2qg0ayfs1j-marked-on-track-by-mitche-injqjvh1.md) read "marked not-started" and "marked on-track". The wake itself was fair, because the building's key result really changed place. Its label was wrong. There is no UI fix to make: GoalsTab and the sheet already guard against sending the same status.
- **Fix, PR https://github.com/mitchellgordon95/muster-town/pull/153, merged as efbd78f:**
  1. `wakes.ts`: a goal-tree move now writes "Key result X moved by Mitchell", with "Now under goal …", "Was under goal …" and "Status unchanged".
  2. `grants.ts updateKeyResult`: re-marking the current status with no new note returns the key result unchanged. It writes nothing, appends no `kr.updated` event and wakes no one. The same status with a new note is still a real update. Met/missed rules and the postmortem queueing are untouched.
  3. Two tests added in `core/test/wakes.test.ts`, and the `docs/wakes.md` row updated. Typecheck passes, the core tests pass (528/528) and CI is green.
- **Should be live:** efbd78f (redeploy queued about 04:30Z). One-line check: a same-status PATCH /api/key-results/:id with no note returns 200, and `GET /api/events?since=<last id>` shows no new kr.updated event.

## What I need from you
Nothing needed.
