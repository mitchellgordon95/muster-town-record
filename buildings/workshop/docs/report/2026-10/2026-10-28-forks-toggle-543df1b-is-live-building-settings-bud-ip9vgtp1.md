---
id: "dc_geip9vgtp1"
type: "report"
state: "building"
title: "Forks toggle (543df1b) is live: Building → Settings → Budget mode has the Forks switch"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Forks toggle 543df1b live and verified (health, bundle, forks=true). LIVE = 543df1b. The forks paragraph leaves the Scheduled with Mitchell FYI next."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T18:33:23.261Z"
sessionId: "se_3462v7enyp"
assignmentId: "as_2sxk0wk9bh"
costUsd: 0.276673
tokens: 13834
turns: 9
createdAt: "2026-10-28T18:33:09.831Z"
updatedAt: "2026-10-28T18:33:23.261Z"
---
## What I did
Checked the live server and its bundle for 543df1b (as_3q116q6coa, report [dc_vaqwy8ykpz](2026-10-28-forks-toggle-added-to-building-settings-budget-mod-qwy8ykpz.md)).

## Findings
- GET /api/health commit = 543df1b, so the change is live.
- The live bundle /workshop/assets/main-BVTUdstj.js contains the Forks field with the hint "Queued building work runs on forks of the manager". It sits right after the "Save budget mode" button code in the Budget mode section.
- GET /api/buildings/workshop returns forks = true, which matches Mitchell's manual flip. Turned on, the toggle shows this value.
- I haven't seen it in a browser because there is no browser on my desk. Mitchell can open Building → Settings for the Workshop and should see Forks switched on.

## What I need from you
Nothing needed.
