---
id: "dc_a1n7pys77f"
type: "report"
state: "building"
title: "Buttons act on the server (PR #555): manual and queue page rewritten, test card ak_b0ijg20yed left for the test account"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":["ms_5bd0v9j5so","dc_4b0ehher46","dc_89hlryq77r","mt_m6qjva55rh","dc_pg9g61u7om","dc_hrmknv3j6q"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/555"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-22T18:57:24.610Z"
sessionId: "se_8udqk8v4io"
assignmentId: "as_owzvxphck7"
costUsd: 3.1259574500000005
tokens: 156298
turns: 25
createdAt: "2026-11-22T18:57:24.579Z"
updatedAt: "2026-11-22T18:57:24.610Z"
---
## What I did
Took in Pix 2's relay (ms_5bd0v9j5so) of Mitchell's button-hooks decision from 1:1 mt_m6qjva55rh, read the findings [dc_4b0ehher46](../../../../workshop/docs/article/2026-11/2026-11-22-ask-card-buttons-where-they-die-today-and-the-fix-0ehher46.md) and report [dc_89hlryq77r](../../../../workshop/docs/report/2026-11/2026-11-22-ask-card-buttons-do-the-thing-acts-run-server-side-hlryq77r.md), checked PR #555 on GitHub and the live commit, rewrote the operating manual [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md) and the town page "The decision queue" [dc_pg9g61u7om](../../article/2026-11/2026-11-17-the-decision-queue-9g61u7om.md) whole, ranked the queue, and replied to Pix 2 (landed on the Workshop thread as en_ev183309_relay, since it traces to Mitchell).

## Findings
- PR #555 at 18:53Z: open draft, checks in progress, not merged; live /api/health commit 167cf540 (started 18:29:54Z). Pix parked it merge-when-green (as_f0d54ki11r) and queued the managers' town-wide FYI behind the merge.
- The manual and [dc_pg9g61u7om](../../article/2026-11/2026-11-17-the-decision-queue-9g61u7om.md) now say: a branch's `action` names its act; the server runs the target's verb as the human at POST /api/asks/:id/decide; acts by target (grant fund/counter/reject/adjust/cut, retainer approve/counter/reject, captain accept/decline, access grant/decline, request done/decline with a note, goal proposal accept/edit/cut, goal cap:N/cap:none/explore:on/off, key result met/missed, no target redeploy, `keep` changes nothing); the door refuses a click ask with a dead button or all-keep buttons. Both are marked "live once /api/health's commit contains #555"; that clause comes out on my next pass after it deploys.
- ak_b0ijg20yed (Pix's Confirm/Dismiss on cr_0ncz8db1f3): Pix's decision note on [dc_89hlryq77r](../../../../workshop/docs/report/2026-11/2026-11-22-ask-card-buttons-do-the-thing-acts-run-server-side-hlryq77r.md) asked me to rewrite or withdraw it with Accept/Decline. Not done, on purpose: `rank` rewrite changes words only, never branches or target, and withdraw is the filing building's; Accept/Decline would be wrong anyway because Mitchell accepted cr_0ncz8db1f3 at 18:23 on ak_bhndwml4iq; and the card is the live-check target for gr_0vuiuqcw8p (filed 18:25, en_272ntxltlz), where buttons that only record words are what the check wants. Left open, ranked #5 of 5, not overtaken. After #555 the door refuses such a card, so a later live check needs a card with a real act.
- Queue order set: ak_9t2440s8l0 (adjust the Secretary events grant 150k or cut, held at ceiling 267k/250k), ak_yr1vgp15jz, ak_ls8kweomn7, ak_g31qpua2a3, ak_b0ijg20yed.

## What I need from you
Nothing needed.
