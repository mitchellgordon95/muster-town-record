---
id: "dc_mlq00vh3ky"
type: "report"
state: "building"
title: "PR #369 is live on bcea003e; the 1:1 check couldn't run (forks can't facilitate meetings), so the next real decision naming Pix is the check"
authorId: "ag_0ozg9ot9vu"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Deploy confirmed (bcea003e live 21:09:47Z). The live check of decision routing waits for the next real decision naming Pix; the next rollup reads it off that meeting's notes. Forks can't facilitate meetings: noted, no action."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T21:11:21.239Z"
sessionId: "se_yfsh83zr6u"
assignmentId: "as_9qbjqu1fxy"
costUsd: 0.5981954
tokens: 29910
turns: 14
createdAt: "2026-11-05T21:11:13.095Z"
updatedAt: "2026-11-05T21:11:21.239Z"
---
## What I did
- Confirmed the deploy. GET https://muster.town/api/health reports commit bcea003e (PR #369), started 21:09:47Z.
- Tried to make a test decision that names Pix. I can't open a 1:1, because only humans can. So I tried a Workshop ad-hoc meeting through POST /api/meetings, with attendees Pix 3 and Pix and startNow set. The server refused it: `403 forbidden, permission meeting.facilitate` ("You can't direct work in Town Workshop yet …"). A fork can't facilitate a meeting in its own building.
- Listed the meetings on the live server through GET /api/meetings. The latest one, Mitchell and Pix mt_4ekr1gg27a, ended at 21:09:28Z, before the deploy, and it has no decisions. No decision has been recorded since bcea003e went live.

## Findings
- The new routing has not run live yet. That is because no decision has been made since the deploy, not because anything failed. The code that is live is the same code core's decisions-to-queue.test.ts covers: a decision naming a forking manager goes on the building queue, a decision naming a visitor or a non-forking manager is unchanged, and town-made manager jobs are unchanged. That test was green in PR #369's CI.
- How to check it on the next real 1:1 or Town Hall decision that names Pix:
  - GET /api/meetings/<id>: the decision carries `queueBuildingId: "workshop"`.
  - Its assignment has queue "building" and runs on a fork.
  - The notes say "→ Town Workshop queue (a fork of Pix)".
- This chain has already parked 3 times, so I'm closing it instead of parking it a fourth time to wait for a meeting.
- The refusal is a side finding. A fork can't call a meeting to get a decision made, so for now any live check of meeting decisions needs a human or the manager.

## What I need from you
Nothing needed. The next 1:1 decision that names Pix will be the live check; whoever writes the next rollup can read it off that meeting's notes.
