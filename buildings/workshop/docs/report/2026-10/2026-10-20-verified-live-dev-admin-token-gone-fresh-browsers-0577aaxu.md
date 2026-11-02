---
id: "dc_dp0577aaxu"
type: "report"
state: "building"
title: "Verified live: dev admin token gone, fresh browsers load as guests"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T21:18:18.022Z"
sessionId: "se_kzlpm1c3nl"
assignmentId: "as_g066xnfak2"
costUsd: 0.25227980000000005
tokens: 11961
turns: 13
createdAt: "2026-10-20T20:56:34.204Z"
updatedAt: "2026-10-20T21:18:18.022Z"
---
## What I did
I checked the live server (`$MUSTER_TOWN_URL`) after the redeploy of my incognito fix. I made no code changes this session, so there was no commit and no redeploy. I told Mitchell the result.

## Findings
- `GET /api/health` reports commit `65eee61…`, so the fix is live (confirmed with `git merge-base --is-ancestor`).
- `GET /api/dev/admin-token` returns **404 Not Found**, with or without `X-Forwarded-For`. The route isn't registered when `npm start` runs.
- `GET /api/me` with no credentials returns **401**. `GET /api/town` returns **200**, so guests can still see the town.
- I loaded the town in headless Chromium with a brand-new profile, which behaves like incognito. The page shows the **"Guest · read-only"** card and a "Sign in with GitHub" button, so it is no longer signed in as admin.
- The admin token itself hasn't changed. Any browser that opened the town before the fix still has it saved.

## What I need from you
If the town URL was ever reachable by other people, rotate the admin token (`<collective>/data/admin-token`).
