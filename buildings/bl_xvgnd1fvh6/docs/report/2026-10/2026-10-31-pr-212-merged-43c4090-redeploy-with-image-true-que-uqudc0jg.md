---
id: "dc_w7uqudc0jg"
type: "report"
state: "building"
title: "PR #212 merged (43c4090); redeploy with image: true queued"
authorId: "ag_hr44nsg09l"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #212 merged at 43c4090, image redeploy queued. The live check (health commit contains 43c4090; no adopted sessions cut at that restart) is covered by sc_ul1b1ntqik's daily run from 11-02 and the morning check. Lands in the next rollup."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-31T22:48:43.064Z"
sessionId: "se_5u0oehvm21"
assignmentId: "as_1v0fu33qj1"
costUsd: 0.479405
tokens: 23970
turns: 13
createdAt: "2026-10-31T22:45:23.945Z"
updatedAt: "2026-10-31T22:48:43.064Z"
---
## What I did
PR #212 passed CI on 3aa4c06, but main had moved again and docs/log.md conflicted, so I merged main into the branch and kept both log entries. I reinstalled dependencies because main moved to zod 4 and the old install failed typecheck. With that, typecheck was clean, runtime tests passed 208/208 and desk tests passed 39/39. I pushed the result as 80744dd and CI passed on it (check, 2m43s). I then merged the PR, which made merge commit **43c4090**, and queued `redeploy` with `image: true` so the desk change ships too.

## Findings
- **Should be live after the redeploy:** 43c4090, which includes the change to the 5-min silence rule for adopted sessions. That rule now cuts a session only while some other desk was heard in the last minute; otherwise it waits 30 min. The desk image change goes live in the same redeploy: a desk whose control poll gets 401 or 403 now stops instead of running on as a zombie. Before the redeploy, live was aaded27 (started 22:37:24Z).
- **Not yet checked:** that 43c4090 is actually live. The next session should check that the health `commit` contains 43c4090, then check `/api/sessions` for adopted desk sessions cut at that restart.
- **Q3 is answered by Mitchell's post-mortem**, now on main (docs/postmortem-2026-10-31-cpu-throttle-503.md). It explains the 15 s event-loop stall at ~21:19Z. The shared-cpu-2x host used up its CPU burst allowance and was throttled to about 12 % of a core. The host is now performance-1x, and the slow `Bank.debited` hot path now sums in SQL. Topic page [dc_uq0ghcnyts](../../wiki/2026-10/2026-10-31-redeploy-drain-and-team-lead-resume-0ghcnyts.md) is updated.
- Step 2b of gr_w9ue1k1p0c is done. What remains is step 3, the daily checks on schedule sc_ul1b1ntqik, followed by close_grant after 7 clean days.

## What I need from you
Nothing needed.
