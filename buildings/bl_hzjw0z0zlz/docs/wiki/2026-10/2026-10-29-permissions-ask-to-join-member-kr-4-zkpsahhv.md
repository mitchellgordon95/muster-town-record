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
updatedAt: "2026-11-03T03:29:57.983Z"
---
State 2026-11-03 03:27Z: **6e6d663c LIVE** (server started 03:27:30Z): contains step 1 92336d0e and step 2 fc28a1e5; served /workshop/assets/main-CGnAe6si.js has "Let in + direct work" ×2, "is for people who direct work under" ×1, 0 × "Members open one new 1:1 a day". **Step 3 df1cb9e5 on main, CI run 41572063282 was in progress** (earlier main runs cancelled by newer pushes). **gr_cuobjlny6r AT CHECKPOINT** (478,159 / 450,000): kr_v21y6z4tbv, kr_qtmcpalo80, kr_3huiw2mea7 claimed; kr_etn1l9ccpi, kr_t7rw103x6u on-track; top-up 80k asked for the held live checks as_3eqwp4ujnw (card pictures) and as_vpdz73pnlc (Members table live + evidence per KR), then close_grant. Design: a GitHub sign-in is read-only until an admin lets them in (a5026c3; [dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md), [dc_o631yrd4s2](../../report/2026-10/2026-10-26-permissions-half-2-on-main-db3534a-signed-in-visit-31yrd4s2.md)). **Never used live on the Workshop:** one stranger signed in (@edwadli, still visitor); only round trip is Mitchell joining Hollyville. Funnel 30 d at 03:27Z 11-03: 210 views / 2 sign-ins / 1 asked / 1 let in / acted 0.
## Round trip: read these request ids
- Outbox **[dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md)** (main round trip) + **[dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)** (add-on: press Let in + direct work, You're in card, one 1:1, optional Members-table check). [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md) **supersedes [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md) and [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md)**; ignore those two (only a human closes an outbox request).
- 7-day check sc_gy1eruamog (2026-11-07 21:00Z).
## Direct work under <goal> (Mitchell mt_hlizi9wxxc d1; grant gr_cuobjlny6r)
**No permission = no 1:1.** Step 1 (core/server) 92336d0e, live: migration **084** `direct_grants`. `packages/core/src/direct.ts` `canDirect(world, who, buildingId)` = facilitate/review in the building, or captain of its attachment goal or an ancestor, or a `direct_grants` row on one of those (and still a member). Used by createOneOnOne, createMeeting (labs) and lanes.ts humanSource. Server test 'direct work permission gates 1:1s, meetings and directed sources' (packages/server/test/access.test.ts:147) also covers GET /api/members (403 for a plain member) and grant/revoke.
**API:** `POST /api/access-requests/:id/decide {grant, directGoalId?}`; `POST|DELETE /api/members/:userId/direct {goalId}` → `{direct}` / `{removed}` (admin or captain over goal, else 403); `GET /api/members` (admin or any captain) → `{members:[{userId,name,githubLogin,avatarUrl,letInAt,direct:[{goalId,text,grantedBy,createdAt}]}]}`; `/api/me` has `direct:[{goalId,text,how}]`, `directDefaultGoalId` and `directBuildingIds`. Refusal text contains "direct work under". Events: "@x was let in as a member", "@x may direct work under \"<goal>\"", "... may no longer ...".
**Step 2 (web) fc28a1e5, live:** `canTalkToManager` (panels/oneOnOne.ts) = staff or `me.directBuildingIds` (never Town Hall); member callout deleted; a member without it sees one muted line on a manager's Talk tab. Town Hall in-tray AccessRow + admin HUD notice: **Let in** (primary) / **Let in + direct work under <goal short>** / Decline; shared code packages/web/src/panels/letIn.ts. Tests web test/talkToAuthor.test.tsx; server access.test.ts asserts directBuildingIds.
**Step 3 (web) df1cb9e5, on main:** User stats → **Members** section for an admin or captain (details [dc_ze5o8drnl9](../2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md)): Grant <default goal> / Revoke per goal, over web api `members / grantDirect / revokeDirect`; mock mode too. Manual (Joining, "What a member can do"): "an admin or captain grants and revokes it at Let in or in the user stats Members table". Test web statsPanel.test.tsx "members table".
Left: Mitchell's checkpoint decision; then the two live checks and close_grant. Real round trip = outbox above.
## Grants
- gr_fibsfwr4tz (450k): steps 1–3 live. Step 4 = round trip above.
- gr_58n37j410s (500k): AT CHECKPOINT; member 1:1 code (4969557) is superseded by the gate above.
## How to check
curl /api/health commit; POST /api/buildings/<id>/one-on-one as a non-holder → 403 (signed out → 401); GET /api/members signed out → 401; curl /api/join-funnel (`totals.acted`). Bundle: curl /workshop/ for the assets/main-*.js name, then grep it. Screenshots: [dc_bci4l87ab6](2026-10-29-live-verification-on-muster-town-i4l87ab6.md) (mock /api/me with directBuildingIds:[] for a member without the grant; isAdmin + directDefaultGoalId + mocked GET /api/access-requests and GET /api/members for the card and the Members table).
