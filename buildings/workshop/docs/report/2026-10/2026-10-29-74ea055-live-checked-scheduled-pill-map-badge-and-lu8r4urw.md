---
id: "dc_d8lu8r4urw"
type: "report"
state: "building"
title: "74ea055 live-checked: \"scheduled\" pill, map badge and building Scheduled list all show; rollup 30 picture mf_27t5k7tlgg"
authorId: "ag_8p2asxvmrt"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ulx9ni4xry","dc_mhz91klzjk","mt_xywhisvdcm"],"urls":["https://muster.town/api/scheduled","https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "74ea055 live-checked: scheduled pill, map badge, Overview Scheduled list and GET /api/scheduled all confirmed; picture mf_27t5k7tlgg goes into rollup 30. Step 2 (migration 055, PR #78) stays in rollup 30's Needs."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T16:37:02.572Z"
sessionId: "se_c45tbc0rku"
assignmentId: "as_itrc4ge8zo"
costUsd: 0.9212296000000001
tokens: 46061
turns: 27
createdAt: "2026-10-29T16:36:55.484Z"
updatedAt: "2026-10-29T16:37:02.572Z"
---
## What I did
I checked the live server (health commit 74ea055) through the API and in a headless browser as a guest. I tested in the UTC and America/New_York timezones, using the two Workshop items waiting on a time: as_rzgy2cp5xf (20:00Z) and as_0fv79mewnk (20:45Z). Both are still queued, so I didn't need a test item. I took and uploaded the rollup 30 picture, and rewrote the topic page [dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md).

## Findings
Step 1 of scheduled work is **live and working**. No bugs found.

- **API:** `GET /api/scheduled` lists 4 items, soonest first:
  - Workshop: as_rzgy2cp5xf at 20:00Z and as_0fv79mewnk at 20:45Z
  - Prod: as_jdx5qsxasf at 21:20Z and as_rm75w55vd0 at 05:05Z on 10-30
  
  None of the 4 appears in `GET /api/blocked`. That list now holds only 2 waits, neither on a time: one on a grant, one on an assignment.
- **Map:** Pix has a blue "scheduled 2" badge above the red "blocked 1" badge (the blocked one is as_xehdmyo3u3, which waits on Pix 3's Town Hall work).
  - Hovering shows "Pix: 1 queued, can't start; 2 scheduled". Each row gives its run time, e.g. "runs at 16:00 your time · 20:00 UTC".
  - Clicking the badge opens Pix's queue.
- **Assignment cards (Pix → Assignments):** both scheduled items have the blue "scheduled" pill and "runs at 16:45 your time · 20:45 UTC". The third item keeps its red "blocked" pill with its reason.
  - With the browser on UTC, the label shortens to "runs at 20:00 UTC", which is correct.
- **Building panel → Overview:** the "Scheduled 2" section lists both items with their run times and "building queue (a fork runs it)". Clicking a row opens the queue.
- **Picture for rollup 30** (662×213 px; map badge on the left, Scheduled list on the right): ![scheduled badge and list](/api/media/mf_27t5k7tlgg.png) (mf_27t5k7tlgg)
- **Not checked live:** the `town-blockers.py` line (Pix 2 already ran it against the live log, [dc_ulx9ni4xry](2026-10-29-scheduled-work-step-1-work-waiting-on-a-time-now-s-x9ni4xry.md)) and the forks' "Your team" count.
- **Step 2** (recurring schedules, migration 055 on draft PR #78) is still unmerged and waiting for Mitchell's approval. That ask is already set for rollup 30's Needs.

## What I need from you
Nothing needed.
