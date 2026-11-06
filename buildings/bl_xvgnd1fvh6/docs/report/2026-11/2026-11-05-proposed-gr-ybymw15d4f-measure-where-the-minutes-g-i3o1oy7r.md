---
id: "dc_hei3o1oy7r"
type: "report"
state: "building"
title: "Proposed gr_ybymw15d4f: measure where the minutes go from a merge to live on muster.town (analysis + public /api/deploys), no fixes"
authorId: "ag_e4ifdwbzim"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["mt_b0agj3dix8","gr_ybymw15d4f"],"urls":["https://github.com/mitchellgordon95/agent-town/actions/runs/42125299180"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_ybymw15d4f filed per Mitchell's 1:1 (mt_b0agj3dix8); it reaches him in the Town Hall in-tray on its own. Nothing to queue until he decides."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-05T23:24:32.009Z"
sessionId: "se_7x0wysnu4q"
assignmentId: "as_hydyuiyu1v"
costUsd: 0.5937178999999999
tokens: 29686
turns: 12
createdAt: "2026-11-05T23:24:23.075Z"
updatedAt: "2026-11-05T23:24:32.009Z"
---
## What I did
Read Mitchell's 1:1 with Pix (mt_b0agj3dix8), ci.yml, the last 15 main CI runs and the live redeploy events. Then I filed proposal gr_ybymw15d4f (300k tokens, 3 steps, 4 key results) in the Town Hall in-tray. It names no fixes, as Mitchell asked.

## Findings
- **What can be seen today:** GitHub shows when each job starts and ends, and the job summary has one line timing the check. Promote's debounce wait appears only in its log ("waiting 720s…"). The restart phases are town events ("Redeploy: build web … ok", "Redeploy finished … at <sha>"). Nothing joins these per commit, and the time a run spends queued behind the previous main run shows up nowhere.
- **One live sample (from the server and GitHub clocks):** 142e85c was merged at 22:53:49Z. Its main run waited about 1.5 min for the run ahead of it, and the check took 181 s. Promote then slept 720 s for the 15-min debounce, because the server had restarted at 22:55:32Z. The restart took 13 s, and the commit was live at 23:10:45Z. That is 17 min from merge to live, 12 of them waiting. Across the last 6 green main runs, check took 141–242 s and promote took 8–813 s. One sample is not a finding; measuring properly is step 1.
- **Plan (gr_ybymw15d4f):**
  1. A script plus a findings doc that time each phase for 7 days of main commits, with median and p90 per phase, and say which phases the existing data can't time.
  2. Promote records its phases, the server stores them with its own restart phases, and a public `GET /api/deploys` shows them. Each main run's GitHub summary shows the same phases.
  3. After at least 10 live deploys, file an analysis that becomes the input to a separate speed-up proposal.
- **Stop rule:** drop step 2 if the existing data already times every phase, or stop after 2 PR iterations without green CI.

## What I need from you
Fund, counter or reject gr_ybymw15d4f in the Town Hall in-tray.
