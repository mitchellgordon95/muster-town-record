---
id: "dc_ykgewidnhn"
type: "report"
state: "building"
title: "faed70b is live: flags are in /api/town and the red pennant is in the map code; no flag planted since, so pick-up not yet seen"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "faed70b live in 49aeb33; the planted-flag pick-up needs Mitchell to plant one, goes into rollup 18 Needs."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T06:32:31.828Z"
sessionId: "se_o3sqj2jl16"
assignmentId: "as_8h1h0eh8xp"
costUsd: 0.5330045999999998
tokens: 22595
turns: 17
createdAt: "2026-10-27T06:32:09.865Z"
updatedAt: "2026-10-27T06:32:31.829Z"
---
## What I did
Checked the live server against faed70b: the health commit, /api/town, the map bundle, and the event log since the deploy.

## Findings
- **Live:** GET /api/health commit is 49aeb33, and `git merge-base --is-ancestor faed70b 49aeb33` passes. ee536a5 (grant proposals in parallel) is **not** live yet. It has its own pending check, as_hiqqe287fg.
- **/api/town** now has a `flags` field. It is `[]` because no planted flag is waiting with a position.
- **Map code:** the drawFlag pennant (pole #5b4636, red pennant #e0453a) is in the shared chunk /workshop/assets/overview-BcrQkA9e.js. main-DT_AzbOK.js carries the flag state code (`flagsWith`).
- **Not yet seen live:** flagPos on a planted flag, and the doc.updated `flagPickedUp` event from Pix. The event log for 05:47–06:31Z has no flag planted after the deploy, and only humans can plant one. Mitchell's flag [dc_r40dq3znse](../../flag/2026-10/2026-10-27-oh-also-flags-should-also-be-visibly-planted-in-th-0dq3znse.md) was planted before the deploy, so it has no position and is decided from the in-tray as before.
- Wiki dc_b1tgy00ubz is updated.

## What I need from you
Mitchell: if you want the last part checked, plant one flag on the map (press F) while standing on a walkable tile. Then Pix's next session should walk to it and pick it up, and GET /api/events will show the flagPickedUp event.
