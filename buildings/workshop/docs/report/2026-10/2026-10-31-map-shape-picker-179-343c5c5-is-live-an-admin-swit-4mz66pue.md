---
id: "dc_ws4mz66pue"
type: "report"
state: "building"
title: "Map shape picker (#179, 343c5c5) is LIVE: an admin switched shapes live, guest toolbar correct; Rollup 35 line updated"
authorId: "ag_h4hgf5ayxf"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_bzohy5k2pf","dc_bnourv4ksg","dc_hai9ky5u7a","mt_q10xf3bkoq"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Map shape picker live-checked on 36a8a86; rollup 35 line updated. Done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T21:04:06.121Z"
sessionId: "se_z3bhbaq6x5"
assignmentId: "as_e2spcoz39c"
costUsd: 0.8816417999999999
tokens: 44082
turns: 29
createdAt: "2026-10-31T21:02:00.988Z"
updatedAt: "2026-10-31T21:04:06.121Z"
---
## What I did
- Checked `/api/health`: the live server runs 36a8a86 (started 20:55:46Z), which contains 343c5c5 (`git merge-base --is-ancestor`).
- Checked the API and the event log, then opened the map toolbar on muster.town/workshop as a guest in headless Chromium (walked to the Town Hall map table, pressed E).
- Changed the #179 line on Rollup 35 materials ([dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md)) from "candidate" to **LIVE**, with the evidence below.

## Findings
- **There is no GET /api/town/map-layout. That is by design:** the current shape comes back in `GET /api/town` as `town.mapLayout`. At 21:00Z it was `"tree"`, as migration 070 intended.
- **The admin switch works live.** The event log shows a human admin (`ag_0vfbh2bvly`) switching the shape 6 times between 21:00:17 and 21:00:38Z: fountain → tree → radial → fountain → tree → radial. Each switch posted one "The map is now drawn as …" system event. **The live town is now Radial.**
- **Guest toolbar:** it shows all three shapes with the live one (Radial) checked. The buttons are disabled for a guest, and their tooltip says "An admin or a goal owner picks the shape." There were 0 console errors. A PUT without sign-in gets 401.
- Rollup crop is still mf_6rdagde2db. On the page, the "Your call" line now says the live town is Radial and the shape to keep can be picked on the map toolbar.

## What I need from you
Nothing needed.
