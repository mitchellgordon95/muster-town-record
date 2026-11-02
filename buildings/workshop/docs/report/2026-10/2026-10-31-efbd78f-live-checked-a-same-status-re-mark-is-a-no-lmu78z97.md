---
id: "dc_hrlmu78z97"
type: "report"
state: "building"
title: "efbd78f live-checked: a same-status re-mark is a no-op on the live server; the \"moved\" label is on main, not yet seen live"
authorId: "ag_71znh51hl8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_euo9bss83c"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "efbd78f live-checked: same-status no-note PATCH is a no-op live (200, nothing written, no kr.updated, no wake). The \"moved\" label is code-confirmed on main; its live row needs a real human move, which is Mitchell's own action. The permission-check ordering side note is harmless (writes nothing); noted, not assigned."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T04:29:33.893Z"
sessionId: "se_6hdgttbrny"
assignmentId: "as_ptolvr5v5s"
costUsd: 0.4147081
tokens: 20735
turns: 10
createdAt: "2026-10-31T04:29:23.637Z"
updatedAt: "2026-10-31T04:29:33.893Z"
---
When Mitchell accepts a goal-tree move proposal, his in-tray row should now read "Key result … moved by Mitchell" with the new goal, the old goal and "Status unchanged". Re-marking a key result with its current status and no note no longer wakes anyone. API-only change, so no picture.

## What I did
- Checked /api/health against efbd78f.
- Sent a same-status PATCH with no note to kr_hj8wwx0q0w and compared the event log before and after.
- Read the move-label code on main.

## Findings
- **Live:** /api/health reports commit efbd78f118ea (started 2026-10-31T04:28:25Z). `git merge-base --is-ancestor efbd78f <commit>` succeeds.
- **No-op PATCH, confirmed live:**
  - kr_hj8wwx0q0w was not-started under gl_join, with an empty note. I sent `PATCH /api/key-results/kr_hj8wwx0q0w {"status":"not-started"}` and got **200**.
  - The key result came back unchanged: status not-started, `updatedAt` still 04:16:18.487Z, `statusBy` null. Nothing was written.
  - The last event was **69970** before the PATCH and **69974** 20 s after. The 4 new events were 2 agent.tool, 1 agent.thought and 1 meeting.utterance. There was **no kr.updated event and no in-tray wake**.
  - Side note: the no-op return (packages/core/src/grants.ts:724) runs before the permission check (line 735). So a same-status, no-note PATCH returns 200 unchanged for any token, even one that couldn't change the status. It writes nothing, so it is harmless.
- **"moved" label: on main, not seen live.**
  - packages/core/src/wakes.ts:72-75 checks for a move with `p.edited !== true && typeof p.goalId === "string" && p.status === p.from`. It then labels the row "moved", with "Now under goal …", "Was under goal …" and "Status unchanged (…)".
  - The docs/wakes.md row (line 40) matches the code.
  - I didn't provoke a move, as the assignment said, so the live row still needs a real human move.

## What I need from you
Nothing needed.
