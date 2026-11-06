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
updatedAt: "2026-11-05T20:01:39.663Z"
---
State 2026-11-05 20:01Z (live 62cf39f2): the join round trip (gr_fibsfwr4tz step 4, kr_bf2df18aa1; gr_cuobjlny6r kr_t7rw103x6u) is now **ours to run with a test GitHub account** (Mitchell, mt_6kz0prkq8l; FYI [dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md)). Chain as_67ks5dtrf6 is parked waiting for the secret `MUSTER_TEST_GH_TOKEN` (not on the desk at 20:01Z). No outbox request, no message to Mitchell about it; backstop sc_gy1eruamog (2026-11-07 21:00Z).
## Not done yet (checked 2026-11-05 20:01Z)
- Workshop has had no real round trip: /api/join-funnel workshop 30-day totals signIns 1, asked 0, letIn 0, acted 0. Town totals asked 1 / letIn 1 = Mitchell joining Hollyville.
- Author-withdraw of outbox requests (Workshop as_b784e3w2g5) not on origin/main 565a075a. When it lands: withdraw **[dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md)** (author retired fork Kelly 2 ag_ugdmxfaxnz; claimed by Mitchell 19:50Z) and **[dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)**, note "superseded by the test-account run ([dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md))". If refused (author-only / claimed), leave and say so; never file replacements. dc_ulla3hu21p, dc_fvlt8xajnz are dead.
## Test-account recipe (never print the token)
1. `POST https://muster.town/api/auth/github/device` `{"accessToken": $MUSTER_TEST_GH_TOKEN}` → user bearer (server auth/routes.ts:63-70).
2. `GET /api/me`: must have no roles; if member/admin, stop (not a stranger).
3. `/api/join-funnel` with a browser UA (`curl -A "Mozilla/5.0 ... Chrome/130"`) before; baseline 20:01Z workshop signIns 1, asked 0.
4. `POST /api/access-requests` (routes/town.ts:114) = Ask to join; GET /api/access-requests as Kelly's agent token → 403, so check the pending request via /api/events ("<who> asked to join", core access.ts:56). Funnel: signIns +1, asked +1 (kr_fbef01cccb).
5. Let in needs town.manage_roles (core access.ts:67) = Mitchell only. Park; rollup Needs: "Press Let in + direct work under the Onboarding goal on the test account's pending request in your in-tray".
6. After let in: /api/me (member, direct), Say once as the account (acted +1), open a 1:1 with a manager (kr_t7rw103x6u); events show "was let in as a member" (access.ts:89) and the Say. Record handle + minutes Ask→Let in. No role reset exists: report roles picked up.
## Direct work under <goal> (Mitchell mt_hlizi9wxxc d1)
**No permission = no 1:1.** `canDirect(world, who, buildingId)` (core direct.ts): facilitate/review in the building, captain of its goal or an ancestor, or a direct_grants row (migration 084), still a member. API: `POST /api/access-requests/:id/decide {grant, directGoalId?}`; `POST|DELETE /api/members/:userId/direct {goalId}`; `GET /api/members` (admin/captain); `/api/me` has `direct`, `directDefaultGoalId`, `directBuildingIds`. Web: panels/letIn.ts, panels/oneOnOne.ts canTalkToManager, StatsPanel MembersTable, youreIn.ts.
## Earlier evidence (gr_cuobjlny6r, live since 111e0bfd)
UI re-check as_ispx6885mz: Let in notice, in-tray card, You're in card, Members table pass at 1400×900 and 390×844 (mocked). kr_v21y6z4tbv, kr_etn1l9ccpi, kr_qtmcpalo80, kr_3huiw2mea7 evidenced; kr_t7rw103x6u waits on the round trip above.
