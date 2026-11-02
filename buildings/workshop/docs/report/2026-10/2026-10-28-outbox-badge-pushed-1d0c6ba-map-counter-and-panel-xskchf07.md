---
id: "dc_r4xskchf07"
type: "report"
state: "building"
title: "Outbox badge pushed (1d0c6ba): map counter and panel title show unclaimed requests; also fixed a duplicate 050 migration that would have crashed prod"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved; continuation parked on 1d0c6ba for the live check. Thanks for catching the duplicate 050."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T02:04:25.932Z"
sessionId: "se_hagk5ty12l"
assignmentId: "as_pu6ziel6p3"
costUsd: 1.7913184000000004
tokens: 89566
turns: 62
createdAt: "2026-10-28T02:03:11.877Z"
updatedAt: "2026-10-28T02:04:25.932Z"
---
## What I did
Built Mitchell's flag [dc_bavivcfmiz](../../flag/2026-10/2026-10-27-the-outbox-should-have-a-notification-badge-with-t-vivcfmiz.md) and pushed it to main as **1d0c6ba**. A redeploy is queued. I parked this on the deploy so the next session can check it live.

## Findings
- **The count:** outbox requests with `requestStatus = 'open'`. Claimed, done and deleted requests don't count. The count is on the snapshot (`GET /api/town` → `outbox`). The server also sends a new WS frame `{type: "outbox", open}` whenever a request is filed, claimed, finished or deleted. Requests are only reachable from the map, so the count is a red badge (`drawBadge`, the same one as the in-tray) on the outbox counter. It also shows as a pill next to the Outbox panel title. The mock server does the same.
- **Test:** core/test/verbs.test.ts files 3 requests, then claims one, finishes it, claims another and deletes one. The frames read 1,2,3,2,2,1,0 and the snapshot ends at 0. The full core and server suites pass (494 tests) and typecheck is clean. docs/manual.md's Outbox line now describes the badge.
- **Problem found on main:** step 4 (44e0451) added `050_topic_pages.sql`, but `050_desk_slots.sql` already had that number. `migrate()` tracks migrations by number, so a fresh DB skipped topic_pages and failed the `docs.topicOf` column check. Prod would have failed to boot on the next redeploy. I renamed the file to 051 and made `migrate()` refuse two files with the same number (**2f39f71**). Someone else then fixed the v12 test (d4fccbb, 2a3db42). I told Lena.
- **Not yet checked live:** whether health contains 1d0c6ba, whether `GET /api/town .outbox` matches the number of open requests in `GET /api/docs?type=request`, and whether the badge shows on the map.

## What I need from you
Nothing needed. This resumes when 1d0c6ba is live, for the live check.
