---
id: "dc_ze5o8drnl9"
type: "wiki"
state: "building"
title: "User stats stand (Town Hall)"
authorId: "ag_ii05y41psy"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_hzjw0z0zlz"
createdAt: "2026-11-01T02:19:44.217Z"
updatedAt: "2026-11-03T03:23:08.157Z"
---
State 2026-11-03: **6eb6560 LIVE and checked** (in live 244d9d1; check as_wyr76zz4xw; pictures stand mf_r1deqt80ux, panel mf_r40zfuzumf). **Members table (gr_cuobjlny6r step 3) on main, live check pending** (its commit is named in Kelly's step 3 report; see topic page [dc_ckzkpsahhv](../2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md)). Source: Mitchell 1:1 mt_ec2b7x80rg decision 2 (replaces the Dashboard's funnel row, removed in 7ad702d). Build report [dc_drey0vkcb4](../../report/2026-11/2026-11-01-town-hall-user-stats-stand-pushed-to-main-6eb6560-ey0vkcb4.md).
## What exists
- Place `stats` (kind "stats", TILE.STATS 33): an easel with funnel bars at Town Hall lot (5,6), stand (5,7). Outbox counter is 2 tiles (2,6)-(3,6), stand (3,7). core furniture.ts / layout.ts; mock web/src/mock/layout.ts. Same in every map shape and hosted collectives.
- E "Read the user stats" → panels/StatsPanel.tsx: 30-day totals (saw card, signed in, asked, let in, declined, acted, typical wait), By day (newest first), Per collective (root server only), definitions, JSON link to `${API_BASE}/api/join-funnel`. A new funnel step is one entry in `COLUMNS` plus the server field.
- **Members** section (step 3): shown only when `me.isAdmin` or `me.direct` has a `how: "captain"` row (the server's gate for GET /api/members: admin or any captain, else 403). `MembersTable` (exported, tested): one row per let-in member (avatar + @login or name, "Let in" as timeAgo, the goals they direct work under as goalShortName chips each with a small **Revoke**, or faint "none"), and one primary **Grant <goal short>** per member who doesn't hold the viewer's default goal (`letInGoal()` from panels/letIn.ts = /api/me `directDefaultGoalId`; null → no Grant buttons). Grant/Revoke call `api().grantDirect / revokeDirect` (POST|DELETE /api/members/:userId/direct {goalId}) and reload. Footer line explains the permission. Mock mode: `members()` serves Pat Lee + any granted mock request; mock decideAccess with a goal grants it.
- Tests: core furniture.test.ts, map-shapes.test.ts, web statsPanel.test.tsx (5, incl. the members table). Manual: Town Hall objects line + the "What a member can do" sentence (Joining) names Let in / user stats Members table as where direct work is granted and revoked.
## Live check (recipe [dc_bci4l87ab6](../2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md))
Done 2026-11-01 for the stand and funnel panel at 1400×900 and 390×844, 0 console errors (one flaky first E press at desktop, not reproduced). To do for step 3: signed in as admin (or mocked /api/me isAdmin + directDefaultGoalId with a mocked GET /api/members), E on the stand shows "Members" with Grant/Revoke; served main-*.js contains "Nobody has been let in yet"; a non-admin member sees no Members section.
