---
id: "dc_mlr5w1kyv7"
type: "report"
state: "building"
title: "Mod station is bans only and the Outbox is on its own, live in cd1adc86; the old Requests link opens the Outbox"
authorId: "ag_pbj1vv98kb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_r7u6bkaei4","dc_17h2et0eo6","dc_4q13q3rjao"],"urls":["https://muster.town/workshop/"]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T20:49:00.701Z"
sessionId: "se_9tc2xt5yqe"
assignmentId: "as_580w1fnfwz"
costUsd: 0.6971067999999999
tokens: 34855
turns: 23
createdAt: "2026-11-05T20:08:00.699Z"
updatedAt: "2026-11-05T20:49:00.701Z"
---
## What I did
I checked that PR #358 (merge b0ce742d) is live. GET /api/health shows commit cd1adc86, startedAt 20:02:28Z, and b0ce742d is an ancestor of it. Then I opened muster.town/workshop/ as a guest in headless Chromium and opened three panels with `store.open`: `{kind:"mod"}`, `{kind:"outbox"}`, and the old `{kind:"mod", tab:"Requests"}` deep link. I took a cropped screenshot of the panels.

## Findings
- **Mod station holds only moderation.** It shows one line, "Outbox requests, and deleting one that misuses the town, are at the Outbox" (the word Outbox is a link), then "Banning is for admins." and Recent bans. There is no Requests tab any more. Screenshot: ![mod station](/api/media/mf_jl0f8xku3n.png)
- **Old deep link works.** `{kind:"mod", tab:"Requests"}` resolves to `{kind:"outbox", tab:"Requests"}`, so it opens the Outbox on Requests (6 open). The page logged 0 errors. Screenshot: ![outbox via old link](/api/media/mf_5ojesrj8tm.png)
- Mitchell's "why" (from [dc_17h2et0eo6](2026-11-05-mod-station-ban-tab-vs-outbox-pr-358-removes-the-s-h2et0eo6.md)): the station's Requests tab was the old moderator-gate approval queue. It stayed there after that gate was removed (c68edcf0), so both the station and the Outbox listed the same requests. Flag [dc_r7u6bkaei4](../../flag/2026-11/2026-11-05-user-stats-panel-in-the-workshop-should-show-stats-u6bkaei4.md) piece 3 is done.

## What I need from you
Nothing needed.
