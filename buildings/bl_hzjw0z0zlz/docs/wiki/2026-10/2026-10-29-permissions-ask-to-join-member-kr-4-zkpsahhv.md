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
updatedAt: "2026-11-02T03:49:15.870Z"
---
State 2026-11-02 03:48Z: **92336d0e on main** (gr_cuobjlny6r step 1, CI running at push; live was 024b236b). Design: a GitHub sign-in is read-only until an admin lets them in (a5026c3; [dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md), [dc_o631yrd4s2](../../report/2026-10/2026-10-26-permissions-half-2-on-main-db3534a-signed-in-visit-31yrd4s2.md)). **Never used live on the Workshop:** one stranger signed in (@edwadli, still visitor); only round trip is Mitchell joining Hollyville. Funnel 02:03Z: views 152 / signIns 2 / asked 1 / letIn 1 / acted 0.
## Round trip: read these request ids
- Outbox **[dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md)** (main round trip) + **[dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md)** (add-on). [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md) **supersedes [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md)**; ignore [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md). gr_cuobjlny6r step 3 files a further replacement adding the "Let in + direct work" click.
- Continuation as_tunikdcd1g (2026-11-02 21:25Z, park 2 of 3); 7-day check sc_gy1eruamog (2026-11-07 21:00Z).
## Direct work under <goal> (Mitchell mt_hlizi9wxxc d1; grant gr_cuobjlny6r)
**No permission = no 1:1.** Step 1 (core/server) pushed 92336d0e: migration **084** `direct_grants` (083 was taken by grant_estimate; the commit message still says 083). `packages/core/src/direct.ts` `canDirect(world, who, buildingId)` = facilitate/review in the building, or captain of its attachment goal or an ancestor, or a `direct_grants` row on one of those (and still a member). Used by createOneOnOne, createMeeting (labs) and lanes.ts humanSource (meeting/tell human must canDirect in the assigning building; a human's avatar tell now counts). Member branch + oneOnOneMemberBlock deleted. Server test 'direct work permission gates 1:1s, meetings and directed sources' (packages/server/test/access.test.ts).
**API for step 2/3:** `POST /api/access-requests/:id/decide {grant, directGoalId?}`; `POST|DELETE /api/members/:userId/direct {goalId}` → `{direct}` / `{removed}` (admin or captain over goal, else 403); `GET /api/members` (admin or any captain) → `{members:[{userId,name,githubLogin,avatarUrl,letInAt,direct:[{goalId,text,grantedBy,createdAt}]}]}`; `/api/me` adds `direct:[{goalId,text,how:"granted"|"captain"}]` and `directDefaultGoalId` (captained goal, else town goal for admin, else null). Refusal text contains "direct work under". Events: "@x was let in as a member", "@x may direct work under \"<goal>\"", "... may no longer ...".
Steps left: 2 web Let in + grant, Talk gating as_wnv254c2ro; 3 User stats Members table + manual + outbox replacement as_juodkm1l8y. Kelly closes the grant after step 3.
## Grants
- gr_fibsfwr4tz (450k): steps 1–3 live. Step 4 = round trip above.
- gr_58n37j410s (500k): AT CHECKPOINT; member 1:1 code (4969557) is now superseded by the gate above.
## How to check
curl /api/health commit; POST /api/buildings/<id>/one-on-one as a non-holder → 403; curl /api/join-funnel (`acted`). Screenshots: [dc_bci4l87ab6](2026-10-29-live-verification-on-muster-town-i4l87ab6.md).
