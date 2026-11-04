---
id: "dc_ti9hz5fu42"
type: "report"
state: "building"
title: "Proposal card fix is live: gr_cwwtrabt2o no longer shows gr_ikgaundf5p's checkpoint lines"
authorId: "ag_y0xlvuvuo3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "b6f66b7 (PR #325) live in 2adb84c; gr_cwwtrabt2o's card clean. Chain as_q6flpqvv8y done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:19:30.058Z"
sessionId: "se_ojzhono6x1"
assignmentId: "as_x636apfm0d"
costUsd: 0.3995085
tokens: 19975
turns: 13
createdAt: "2026-11-04T19:19:00.144Z"
updatedAt: "2026-11-04T19:19:30.058Z"
---
## What I did
- Checked that b6f66b7 (PR #325) is live. /api/health at 19:18:31Z showed commit 2adb84c, and b6f66b7 is an ancestor of it.
- Read the open Workshop proposal gr_cwwtrabt2o through the live API.
- Rewrote the topic page [dc_zlj7dltlp4](../../wiki/2026-11/2026-11-04-exploration-2026-11-04-grant-bookkeeping-cost-gr-k-j7dltlp4.md) and logged one line.

## Findings
- GET /api/grants/gr_cwwtrabt2o returns `evidence: null` and `continues: null`, and the response never mentions gr_ikgaundf5p.
- The in-tray card shows the "earlier grant stopped at its checkpoint" block only when `evidence` is set (packages/web/src/panels/Places.tsx:726). So the stray lines Mitchell saw in 1:1 mt_z1b38bwg98 are gone.
- I checked this through the API, not on screen: this desk has no headless browser.
- From now on a proposal shows a predecessor's evidence only when it names that predecessor with `continues`.
- This chain (as_q6flpqvv8y) is done.

## What I need from you
Nothing needed.
