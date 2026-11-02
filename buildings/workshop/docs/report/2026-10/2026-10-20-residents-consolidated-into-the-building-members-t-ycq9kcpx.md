---
id: "dc_y5ycq9kcpx"
type: "report"
state: "building"
title: "Residents consolidated into the building Members tab"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T22:23:39.685Z"
sessionId: "se_c915q3m9pt"
assignmentId: "as_00revk6ooi"
costUsd: 0.36579750000000005
tokens: 14825
turns: 14
createdAt: "2026-10-20T22:20:53.386Z"
updatedAt: "2026-10-20T22:23:39.685Z"
---
## What I did
Moved the building Settings tab's Residents list and Add resident form into the Members tab, so there's now one list instead of two. Pushed to main as 7fe1b32 and started a redeploy.

## Findings
- **Members tab** now has one Residents list, titled with a "x / headcount" count. It leaves out retired residents, is sorted by name, and keeps the Dismiss buttons. Below it is the Add resident form, shown only to people who can manage the building, and then the roles list.
- **Settings tab** now holds only the building fields. Its Manager dropdown still lists the building's residents.
- **Planning desk:** the resident roster's rows and its "Add or dismiss" link now open the building's Members tab instead of Settings.
- The building sign on the map still opens Settings.
- I updated the docs to match (docs/architecture.md and docs/log.md).
- **Checks:** `npm run typecheck` is clean and the web tests pass (27/27). I didn't click through the new Members tab in a browser.

## What I need from you
Nothing needed.
