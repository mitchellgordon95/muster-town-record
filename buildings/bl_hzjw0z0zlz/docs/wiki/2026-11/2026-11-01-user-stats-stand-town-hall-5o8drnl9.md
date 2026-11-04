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
updatedAt: "2026-11-04T00:31:53.369Z"
---
State 2026-11-04 00:31Z: **Members table (gr_cuobjlny6r step 3, df1cb9e5) LIVE and checked** in db2b9ddf (as_vpdz73pnlc). **Follow-up 824ab4d on main** (CI run 41747442043 started 00:31Z; live when /api/health commit contains it): the check found "Grant <goal>" clipped by the panel edge at 390×844 AND 1400×900, so the button is now just **Grant** inside the "Direct work under" cell and the goal is named once above the table ("Grant gives direct work under “<short>”."). Stand itself live since 6eb6560 (pictures mf_r1deqt80ux, mf_r40zfuzumf). Source: Mitchell 1:1 mt_ec2b7x80rg d2. Build report [dc_drey0vkcb4](../../report/2026-11/2026-11-01-town-hall-user-stats-stand-pushed-to-main-6eb6560-ey0vkcb4.md).
## What exists
- Place `stats` (kind "stats", TILE.STATS 33): easel at Town Hall lot (5,6), stand (5,7). Same in every map shape and hosted collective. E "Read the user stats" → panels/StatsPanel.tsx: 30-day totals, By day, Per collective (root only), definitions, JSON link to /api/join-funnel. A new funnel step = one `COLUMNS` entry + the server field.
- **Members** section: only when `me.isAdmin` or `me.direct` has `how: "captain"` (the server gate on GET /api/members: else 403; signed out 401). `MembersTable`: per let-in member avatar + @login, "Let in" timeAgo, a `.member-direct` cell with each held goal (goalShortName chip + small Revoke) or faint "none", then a primary **Grant** when they don't hold the viewer's default goal (`letInGoal()` = /api/me `directDefaultGoalId`; null → no Grant, no caption). Calls `api().grantDirect / revokeDirect`. Mock mode: `members()` serves Pat Lee (mock caption shows "gl_town": the mock has no plaza for it; live shows the goal name).
- Tests: web statsPanel.test.tsx (5, incl. "members table"), core furniture/map-shapes. Manual (Joining): "an admin or captain grants and revokes it at **Let in** or in the **user stats** Members table".
## Live check recipe
[dc_bci4l87ab6](../2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md). Desk script ~/lc7/shot.mjs (Kelly 1's desk; cache only): puppeteer on live /workshop/, intercept GET /api/members with 2 fake members, refuse every non-GET /api/*, set `musterTown.store` me {isAdmin, direct, directDefaultGoalId:'gl_town'}, walkTo('stats'), press E. Expected noise only: 403 on the refused POST /api/join-funnel/view, and 401 on GET /api/access-requests (mocked admin is really signed out).
