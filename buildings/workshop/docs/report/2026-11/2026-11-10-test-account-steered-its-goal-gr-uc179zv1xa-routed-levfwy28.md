---
id: "dc_jklevfwy28"
type: "report"
state: "building"
title: "Test account steered its goal (gr_uc179zv1xa routed to it, canDecide true); first live reset ran at 17:20:15Z, account is visitor-only again"
authorId: "ag_uookgzbo3b"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Steer check passed (routes[gr_uc179zv1xa] mine+canDecide as the account, defaultView mine) and the first live reset ran clean at 17:20:15Z (visitor only, ownerId cleared, access request deleted). All four key results now have evidence (tests: packages/core/test/captain-requests.test.ts and packages/server/test/captain-requests.test.ts): closing gr_bwm0iz7rwl as done and rolling up. Nothing to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T17:21:26.490Z"
sessionId: "se_ld3ofdhw1i"
assignmentId: "as_62lpwynu0z"
costUsd: 1.0067292
tokens: 50336
turns: 18
createdAt: "2026-11-10T17:20:56.054Z"
updatedAt: "2026-11-10T17:21:26.490Z"
---
## What I did
I signed in as dungeonrpg99-ops (us_u4mzpz4zc7) with the test-account skill ([dc_11e758uhzj](../../../../../library/skill/2026-11/2026-11-06-test-account-live-check-e758uhzj.md)). The token was never printed. Mitchell had already accepted cr_6xfa4ka7bq, so I ran the steer check as the account, read-only. I did not touch gr_uc179zv1xa. Then I checked the event log for other checks on the account, ran the first live `POST /api/me/reset` and read the state again. I rewrote topic pages [dc_leh1izdur3](../../wiki/2026-10/2026-10-31-ask-to-captain-a-goal-gr-bwm0iz7rwl-h1izdur3.md) and [dc_jix89oy4ve](../../wiki/2026-11/2026-11-06-test-github-account-dungeonrpg99-ops-x89oy4ve.md).

## Findings
**Part A: steer check (kr_917dc5ba6d). It passes.**
- On GET /api/goals, ob_508f35a2m4 has ownerId us_u4mzpz4zc7 and owner name dungeonrpg99-ops. Its last update was 2026-11-06 05:55:33Z, which is when Mitchell accepted.
- Before the reset, `me` showed captains [ob_508f35a2m4] and roles visitor+member.
- As the account, GET /api/buildings/town-hall/intray returned `defaultView: "mine"`. Outreach's proposed grant gr_uc179zv1xa (under ob_508f35a2m4, asks 180,000) is routed to the account: `{goalId: ob_508f35a2m4, mine: true, canDecide: true}`. In the web code, DecisionQueue.tsx:284 and ReviewDeck.tsx:53 pass `routes[id].canDecide` to GrantRow, which renders Fund/Counter/Reject.
- Not checked: whether a rollup filed against that goal reaches the account. No building is attached to ob_508f35a2m4, so no rollup is routed to it.
- kr_j1w17nw178 is now proven end to end: a member asked to captain (11-06), the captain accepted, ownerId was set, and the new captain could steer.

**Part B: first live reset (time read from server /api/health).**
- No other check was in flight. The event log from 11-09 22:36Z to 11-10 17:20Z shows no use of the account, only two open human asks about it: ak_tvtkj0lzty (Onboarding, optional "direct work under") and ak_964oxnm14w (a GitHub repo for it). Onboarding's join check finished on 11-06 ([dc_tbna71956d](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-06-join-round-trip-done-dungeonrpg99-ops-asked-at-04-na71956d.md)).
- **Before**, at 17:20:14Z: roles [role:visitor, role:member], canInteract true, accessRequest granted (Mitchell), captains [ob_508f35a2m4], directGoals [], visitorAgents [] (ag_tgir6hsxv3 had already been retired).
- **Reset**: HTTP 200 `{rolesRemoved:[role:member], goalsReleased:[ob_508f35a2m4], accessRequestsDeleted:1, captainRequestsWithdrawn:0, directGrantsRemoved:0, agentsRetired:[]}`. 0 captain requests were withdrawn because cr_6xfa4ka7bq had been accepted, so none was pending.
- **After**, at 17:20:15Z: roles [role:visitor], canInteract false, accessRequest null, captains [], directGoals []. ob_508f35a2m4 ownerId is null and the goal now inherits Mitchell from gl_town. The account's in-tray now opens on "all", and routes[gr_uc179zv1xa] = Mitchell with canDecide false.
- GET /api/users/us_u4mzpz4zc7, which the assignment named, does not exist (404). A human can check the roles in the Town Hall instead.
- The account is free. A future check that needs member has to ask to join again and get Mitchell's Let in.

kr_07d30db2bf (tests) and kr_fd3ac479eb (in-tray row and deck slide) got no new evidence this session. Pix can close the grant from the earlier steps' evidence.

## What I need from you
Nothing needed.
