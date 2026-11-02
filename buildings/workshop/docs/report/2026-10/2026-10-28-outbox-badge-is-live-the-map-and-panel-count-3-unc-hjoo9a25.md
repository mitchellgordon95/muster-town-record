---
id: "dc_tmhjoo9a25"
type: "report"
state: "building"
title: "Outbox badge is live: the map and panel count 3 unclaimed requests, which matches the request list"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Mitchell's flag dc_bavivcfmiz is done: badge live at 6a93861, count 3 matches the open requests. Goes in rollup 27."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T02:09:21.554Z"
sessionId: "se_4ls21yp8vx"
assignmentId: "as_7g00z58g7v"
costUsd: 0.33922990000000003
tokens: 16961
turns: 11
createdAt: "2026-10-28T02:09:10.665Z"
updatedAt: "2026-10-28T02:09:21.554Z"
---
## What I did
Checked prod for Mitchell's outbox badge flag ([dc_bavivcfmiz](../../flag/2026-10/2026-10-27-the-outbox-should-have-a-notification-badge-with-t-vivcfmiz.md)):
- the health commit,
- the count in GET /api/town against the request list,
- the live web bundle.

## Findings
- **The badge commit is live.** GET /api/health reports commit 6a93861, and `git merge-base --is-ancestor 1d0c6ba 6a93861` succeeds, so 1d0c6ba is included.
- **The count matches.** GET /api/town returns `outbox: 3`. GET /api/docs?type=request lists 7 requests: 3 open, 1 claimed, 2 done and 1 rejected. The 3 open ones are [dc_kcjl97d3os](../../../../../town-hall/outbox/2026-10/2026-10-27-start-fund-and-retire-a-collective-with-a-second-g-jl97d3os.md), [dc_3oslgrfo6j](../../../../../town-hall/outbox/2026-10/2026-10-27-sign-in-once-on-muster-town-and-confirm-your-role-slgrfo6j.md) and [dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md).
- **The live web bundle has all the badge code.** /workshop/assets/main-2sE0VV-4.js contains:
  - the code that draws the badge on the tile above the outbox place;
  - the handler for the `outbox` update message (`case"outbox"`), which keeps the count current when a request is filed, claimed, finished or deleted;
  - the Outbox panel title's warning pill, "Requests nobody has claimed yet".
- **I haven't seen the badge drawn on the map.** My desk has no browser, so I couldn't load the page as Mitchell would. With the current data it should show **3**.

## What I need from you
Nothing needed.
