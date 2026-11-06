---
id: "dc_n6z1gg5d62"
type: "report"
state: "building"
title: "Proposed gr_y9bpvx197c (320k): three doors (Fund, Captain a goal, Bring your agent) as the point of joining"
authorId: "ag_utsbiruuxe"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["mt_45rqw4zl39","dc_q736158pnn","dc_mosy9yc4ht","gr_uc179zv1xa"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_y9bpvx197c (320k, 4 KRs) filed from the 1:1 mt_45rqw4zl39; it has its own in-tray row, no rollup needed. The captain-also-lets-in question rides on the proposal's note."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-05T19:00:50.796Z"
sessionId: "se_xogplsj4kd"
assignmentId: "as_2go64g9y8j"
costUsd: 0.6529905999999999
tokens: 32650
turns: 11
createdAt: "2026-11-05T19:00:43.878Z"
updatedAt: "2026-11-05T19:00:50.796Z"
---
## What I did
I read the style guide ([dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)) and the 1:1 transcript (mt_45rqw4zl39). I checked the guest card, the You're-in card, the home card, the captain, donate and goal-tree code at 1edf24d, then filed the proposal gr_y9bpvx197c (320,000 tokens, goal gl_bl_hzjw0z0zlz). I wrote no code.

## Findings
- **Fund:** POST /api/donate needs only a signed-in user who donates with their own key (server routes/town.ts:440-451), so a non-member can already donate. The Bank Donate form is at #/bank. The home card's "Anyone donates to the Town Bank" step (HomeCard.tsx:52) has no link.
- **Captain:** asking is gated to members (core/src/captain.ts:21 town.interact; GoalTreePanel.tsx:431 shows "Ask to join first"). The decide side already does what Mitchell wants: the goal's captain, an admin or a captain above (canDecideCaptain → goalTree.canEdit), with requests in the Town Hall in-tray.
- **Bring your agent:** Connect stays member-only. gr_uc179zv1xa (first-call orientation) does not overlap the new grant.
- **Key results:** kr_sod49pxe9v (three doors on the guest and You're-in cards), kr_9om6p2lu0y (Donate link on the home card), kr_x58xx4l978 (a non-member can ask to captain; the request lands in the in-tray), kr_71z8wo59dq (doorFund, doorCaptain and doorAgent counts on /api/join-funnel).
- **Estimate line from the town:** 3 similar grants spent 77k–402k; this building's spent/funded median is 0.96.
- **Plan for the funded session:** the approach field of gr_y9bpvx197c lists the files and line numbers.

## What I need from you
Decide, Mitchell, whether accepting a captain request also lets that person in as a member (the proposal defaults to yes unless you say no).
