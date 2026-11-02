---
id: "dc_e1ui5g2182"
type: "report"
state: "building"
title: "Meeting \"is writing…\" indicator is live (84153bd): drafting endpoint and panel line are served"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: decision 5 item 1 live at 84153bd (drafting endpoint 200, bundle carries the line). First on-screen check happens at the next meeting with agents. Reported to Mitchell in rollup 26."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T00:37:53.824Z"
sessionId: "se_3s40rlrsra"
assignmentId: "as_qwbpbtopj2"
costUsd: 0.28468810000000006
tokens: 14234
turns: 9
createdAt: "2026-10-28T00:37:39.264Z"
updatedAt: "2026-10-28T00:37:53.824Z"
---
## What I did
I checked that 84153bd is running on the live server, Mitchell's item 1 from the town hall (mt_q1w4o85ao9, decision 5). I made no code changes.

## Findings
- `GET /api/health` reports commit `84153bd487bc…`, so the feature is deployed.
- `GET /api/meetings/mt_q1w4o85ao9/drafting` returns 200 `{"drafting":[]}`. The endpoint is up and the list is empty because that meeting is over.
- The live web bundle (`/workshop/assets/main-CGRGL6uU.js`) contains the "is writing" text and the `.utt-writing` style, so the meeting panel can show the line.
- **What it does:** while a meeting is in discussion, the meeting panel shows "X is writing…" under the transcript. An agent gets that line from the moment its listen call returns something new to answer. The facilitator gets it after any listen or status call, which covers the time spent writing decisions. The line goes away when the agent listens again, speaks, decides or ends the meeting, when its session ends, or after 5 minutes. The panel checks for it every 4 s. The meeting status call also lists who is drafting. The details of the change are in [dc_57cv7b5ly4](2026-10-28-meeting-is-writing-indicator-is-on-main-as-84153bd-cv7b5ly4.md).
- **Not yet seen live:** no meeting was running when I checked, so nobody has seen a non-empty drafting list or the line on screen yet. The next meeting with agents will be the first real check. The core meetings tests cover setting and clearing (15/15).

Item 1 of 3 is done.

## What I need from you
Nothing needed.
