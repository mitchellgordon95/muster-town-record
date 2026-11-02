---
id: "dc_8pf4r9o0ax"
type: "report"
state: "building"
title: "gr_cuobjlny6r funded: plan cut into 3 grant-lane steps on the building queue (core/server gate + API now, web Let in + Talk gating after it, User stats + manual + round-trip outbox after that)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_ckzkpsahhv","dc_1g2772fjog","mt_hlizi9wxxc"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Own plan report for gr_cuobjlny6r; its three grant steps (as_pi5gjvlijz → as_wnv254c2ro → as_juodkm1l8y) are already on the queue. Folded into the scheduled rollup sc_w7vz73h9h2 (06:10 UTC)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T03:11:36.286Z"
sessionId: "se_slssl1p4yy"
assignmentId: "as_rjjumy997o"
costUsd: 1.9189809
tokens: 95949
turns: 21
createdAt: "2026-11-02T03:11:21.152Z"
updatedAt: "2026-11-02T03:11:36.286Z"
---
## What I did
Read the grant plan (gr_cuobjlny6r, 450,000 tokens, due 2026-11-09, source Mitchell's decision 1 in mt_hlizi9wxxc) and the permissions topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md), then queued the plan's three steps in lane grant on the building queue, chained with waitFor so each starts when the one before it finishes. No code was written this session; the steps are the work.

- **Step 1** as_pi5gjvlijz (pending now): core/server. Additive migration `direct_grants` (userId, goalId, grantedBy, createdAt); canDirect(user, building) = facilitate/review there, or captain of the building's attachment goal or an ancestor, or a direct grant on one of those. createOneOnOne and createMeeting use it; the plain-member branch and oneOnOneMemberBlock are deleted; humanSource refuses a non-holder's tell or 1:1 as a directed source; decideAccess takes an optional directGoalId; POST/DELETE /api/members/:userId/direct, GET /api/members, /api/me lists direct goals; server test 'direct work permission gates 1:1s, meetings and directed sources'. Parked live check: non-holder POST one-on-one returns 403. Covers kr_3huiw2mea7 and the server halves of kr_qtmcpalo80 and kr_t7rw103x6u. Pages: [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md), [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md).
- **Step 2** as_wnv254c2ro (waits on step 1): web. In-tray AccessRow and admin HUD notice get "Let in" and "Let in + direct work under <goal>" (default the decider's captained goal, else the town goal); Talk gated by what /api/me reports; member callout and isMemberTalk deleted. Parked live check with a cropped picture of the two-button card. Covers kr_v21y6z4tbv and the web half of kr_qtmcpalo80. Pages: [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md), [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md), [dc_xsq7zncdvj](../../wiki/2026-10/2026-10-29-the-stranger-s-first-minute-homepage-workshop-kr-1-q7zncdvj.md).
- **Step 3** as_juodkm1l8y (waits on step 2): User stats Members table (goal or "none", one-click grant/revoke, event logged), one manual line under the 1,900-word cap, and a new outbox request superseding [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md) so the real stranger round trip includes the grant click and a directed assignment from the 1:1. Covers kr_etn1l9ccpi and the live half of kr_t7rw103x6u. Pages: [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md), [dc_ze5o8drnl9](../../wiki/2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md), [dc_k6ueovv1g8](../../wiki/2026-10/2026-10-29-operating-manual-ueovv1g8.md). When it is live I close the grant with close_grant.

Also: on Pix 2's tell, moved the staleness-sweep topic page [dc_1g2772fjog](../../wiki/2026-10/2026-10-29-staleness-sweep-kr-6-2772fjog.md) to checked-through d75b388 (sweep 6, PR #258, lag 0 h). Updated [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) with the funded state and step ids.

## Findings
- The grant's plan already fit three one-session steps; each step is one commit on main with its own parked live check, so there is no separate check step. Join approval stays admin-only, as the plan says.
- The queue ahead of step 1: as_r02o6mvpvt (founder funnel, gr_ngg1z160a8) is pending, and two forks are live (Kelly 1 on the help-signs flag, Kelly 2 on gr_ngg1z160a8 step 1). Step 1 starts when a fork is free.
- Rollup: nothing of this is live yet. The scheduled rollup sc_w7vz73h9h2 (fires 2026-11-02 06:10 UTC) covers ba6cd930, the outbox add-on, and both plan reports ([dc_1fii4mjse4](2026-11-02-gr-ngg1z160a8-funded-plan-cut-into-3-grant-lane-st-ii4mjse4.md) and this one).

## What I need from you
Nothing needed.
