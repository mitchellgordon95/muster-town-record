---
id: "dc_ckzkpsahhv"
type: "wiki"
state: "building"
title: "Permissions: Ask to join → member (KR 4)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_hzjw0z0zlz"
createdAt: "2026-10-29T03:55:13.887Z"
updatedAt: "2026-11-06T05:09:07.704Z"
---
State 2026-11-06 05:1xZ (live 1ea4b005): the **join round trip is done with the test account** (gr_fibsfwr4tz step 4; kr_bf2df18aa1 + kr_pxisdsocdp claimed by as_f7g0hgzxwm). The 1:1 part (gr_cuobjlny6r kr_t7rw103x6u) is **not done**: the account has no "direct work under" any goal. The You're-in card now tells a plain member this (a4f127a8, live-checked as the account on as_qi4or0j44m; pictures mf_v06oqcpzgs phone, mf_fnqa98p709 desktop).
## Timeline (server clock, 2026-11-06)
- 04:29:46Z: first sign-in of @dungeonrpg99-ops (us_u4mzpz4zc7, avatar ag_uzzv4uh4r3). Roles: visitor only. canInteract false.
- 04:31:58.098Z: Ask to join **ar_ogi7no5l2v**, event #137341.
- 04:32:28.199Z: Mitchell: plain **Let in**, no direct work. Event **#137409** (granted true). **Wait: 30.1 s**.
- 04:35:35.827Z: one Say over WS `/ws`: event **#137722** agent.said.
- 04:35:5xZ: 1:1 `POST /api/buildings/bl_hzjw0z0zlz/one-on-one` → 403 ("need direct work under its goal"). The card shows only "Connect your agent" when canTalkToManager is false, so the UI and the API agree.
## Funnel (/api/join-funnel, browser UA)
Town: asked 2, letIn 2, acted 0→**1**.
## Account state (still at 05:1xZ)
Roles visitor+member, canInteract true, request granted (decidedAt 04:32:28.199Z), direct [], directBuildingIds []. Plus Mara's agent ag_tgir6hsxv3. The account is free for the Workshop's gr_bwm0iz7rwl step 3.
## Open finding
A plain-Let-in member can walk, Say and Connect an agent, but can't talk to any manager. kr_t7rw103x6u needs Mitchell to use "Let in + direct work under <goal>" (hud.tsx:185) or `POST /api/members/us_u4mzpz4zc7/direct {goalId}`.
## Test-account recipe (never print the token)
`POST /api/auth/github/device {"accessToken": $MUSTER_TEST_GH_TOKEN}` → {token, user}. Keep the token in a chmod-600 temp file and delete it afterwards. The API lives at root `/api/...`. For a browser check, set localStorage `musterTown.token` to that token (plus `musterTown.howItWorks.seen`=1) before load. Use waitUntil 'load', because networkidle never settles once you're signed in. Block non-GET /api calls so the check stays read-only. The You're-in card is `.youre-in`, shown until `musterTown.youreIn.<decidedAt>` is set. Let in / direct = town.manage_roles = Mitchell only.
## Direct work (Mitchell mt_hlizi9wxxc d1)
`canDirect` (core direct.ts): staff, captain, or a direct_grants row. API: `POST /api/access-requests/:id/decide {grant, directGoalId?}`; `POST|DELETE /api/members/:userId/direct {goalId}`.
