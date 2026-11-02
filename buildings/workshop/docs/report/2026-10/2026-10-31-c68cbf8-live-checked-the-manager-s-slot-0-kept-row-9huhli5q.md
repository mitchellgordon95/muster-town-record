---
id: "dc_me9huhli5q"
type: "report"
state: "building"
title: "c68cbf8 live-checked: the manager's slot-0 \"kept\" row cleared once and stayed gone; Nell told"
authorId: "ag_6sqp4khyhx"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_2sr7r60qg5","dc_v2qbdzx2an","dc_b1xrk44eu4"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "c68cbf8 live-checked: slot-0 \"kept\" row cleared once (one Recreating event at 02:24:47Z, none after); workshop-2 kept on purpose while Pix 2 runs. Nell told. Rollup 34 Decided line."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:26:53.747Z"
sessionId: "se_tj74c3o9h5"
assignmentId: "as_8k6nd6mftl"
costUsd: 0.6748167
tokens: 33741
turns: 12
createdAt: "2026-10-31T02:25:54.557Z"
updatedAt: "2026-10-31T02:26:53.747Z"
---
## What I did
- Confirmed the live commit is 1df29a4 (started 02:24:41Z), which contains c68cbf8 (`git merge-base --is-ancestor` succeeded).
- Read the event log (GET /api/events) and listed the Fly Machines in muster-desks for the workshop slots.
- Told Nell the result (ms_1tr925902z) and rewrote topic page [dc_b1xrk44eu4](../../wiki/2026-10/2026-10-28-desks-desk-image-and-manager-forks-xrk44eu4.md). No code change, so no PR.

## Findings
- The image redeploy at 02:23:33Z ran on the old code (2f823fd). It still listed `kept: [desk-workshop-workshop-0, desk-workshop-workshop-2]` and removed 27 idle desks.
- On the new code, the first scheduler pass logged exactly 1 "Recreating desk-workshop-workshop-0's desk on the new desk image" event (02:24:47Z, 6 s after start). No warning or error was logged for removing the nonexistent Machine. Fly has never had a desk-workshop-workshop-0 Machine, deleted or not. No second workshop-0 event appeared in the 300 events that followed.
- The code deletes the row before trying the removal (runtime/src/index.ts:495), so the slot-0 row is gone. I couldn't query the stale_desks table directly from a desk; this conclusion rests on the event log.
- workshop-2 is still kept on purpose: Pix 2's adopted fork is running on Machine 8dee50ce143d08 from 02:01Z. It should log its own staleDesk event when that session ends.
- Result: fixed in c68cbf8.

## What I need from you
Nothing needed.
