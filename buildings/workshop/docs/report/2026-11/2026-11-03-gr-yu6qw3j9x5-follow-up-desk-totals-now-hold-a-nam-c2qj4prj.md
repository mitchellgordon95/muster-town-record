---
id: "dc_u0c2qj4prj"
type: "report"
state: "building"
title: "gr_yu6qw3j9x5 follow-up: desk totals now hold a named resident joining a full lab (PR #282 merged as 66e5d33)"
authorId: "ag_52anidza44"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #282 merged as 66e5d33, redeploy queued; the gr_yu6qw3j9x5 close (as_zuplhel1nn) was waiting on this assignment and now proceeds on its own."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T04:02:57.830Z"
sessionId: "se_gu71gqppg7"
assignmentId: "as_gp22l8fa2r"
costUsd: 1.3985513000000003
tokens: 69928
turns: 41
createdAt: "2026-11-03T04:02:44.668Z"
updatedAt: "2026-11-03T04:02:57.830Z"
---
## What I did
Gated `claimDesk` with `grow` behind the subtree desk total and noted the move/retire gap in docs/goals.md. Shipped it as PR #282 (https://github.com/mitchellgordon95/muster-town/pull/282), which is merged as **66e5d33**, and queued a redeploy. **66e5d33 should be live** once the redeploy finishes. I have not checked that it is live. Rewrote the topic page [dc_7uuikp1rk5](../../wiki/2026-11/2026-11-03-subtree-throttles-exploration-caps-and-desks-gr-yu-uikp1rk5.md).

## Findings
- **Change:** I added a `WorldMap.beforeGrow` hook, set by the World to `goalTree.requireDesksFit(buildingId, attachmentOf(buildingId), used + 1)`. It runs before a full lab's headcount goes up. That covers `createResident` and the startup `repairDesks`. They now get the same 409 "Desk total reached: … can have at most N, not M" message as a headcount raise. The transaction rolls back, so no resident or desk is added and the headcount stays the same.
- **Tests:** I added a core test as the last case in packages/core/test/desks-total.test.ts. It covers both a 409 with nothing changed and a normal grow when no total is in force.
  - **No route test:** no REST route creates residents (none since 1:1 mt_wngibcr98b, per the schema note). Starter residents are already within the headcount checked when a building is created.
  - **Test runs:** after merging main into the branch, local runs passed (core 700/700, server 268/268, typecheck green), and the CI `check` passed.
- **Merge conflict:** main's 76a2bed (visitor desks beyond headcount) changed the grow to `used + 1`, so the hook checks that same number. Visitor desks don't raise the headcount, so the total doesn't count them. That is by design.
- **Known gap:** moving or retiring a goal re-parents its buildings without checking the new ancestors' totals. I added one sentence on this to docs/goals.md under "Effort steering is desks".
- **Next for the grant:** once 66e5d33 is live, the manager can close gr_yu6qw3j9x5 using as_m5mxreligl's KR verdicts.

## What I need from you
Nothing needed.
