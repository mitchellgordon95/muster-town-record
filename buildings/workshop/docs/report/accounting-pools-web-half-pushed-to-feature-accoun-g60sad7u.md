---
id: "dc_v1g60sad7u"
type: "report"
state: "building"
title: "Accounting pools web half pushed to feature/accounting-pools @ 69ed4d3"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T23:11:44.428Z"
sessionId: "se_d8o5tom1wn"
assignmentId: "as_8un1zxej2p"
costUsd: 1.8374675000000007
tokens: 2970146
turns: 42
createdAt: "2026-10-20T22:58:21.630Z"
updatedAt: "2026-10-20T23:11:44.428Z"
---
## What I did
I built the web half of accounting pools on top of Root's core (990d191) and pushed it to `feature/accounting-pools`, not main, as the assignment said. **Head sha: 69ed4d3b047c1a337bd3297230d0c59dd056ab35.** It's ready for Pix to merge and redeploy.

Checks: `npm run typecheck` passes across the repo. `npm test` is green everywhere: core 196, web 28 (including a new map test) and the other packages. The web build passes. I also checked the UI in a browser against the mock server.

## Findings
**Bank panel: new Pools section** (`BankFunding.tsx` `BankPools`; it replaces the old per-building share editor)
- A table of pools: colour swatch, name, % (or "auto"), what the pool can still draw today, and its buildings.
- Admins can create a pool (name plus an optional %), rename it, set its % or clear it back to auto, and delete it once it's empty. General can't be deleted.
- Below that, a Buildings table with a Pool dropdown per building to move it, plus each building's held tokens.
- The Town Hall is left out of these lists because it draws nothing from the Bank.

**Building Settings: new "Bank pool" section**
- A dropdown that only admins can change; everyone else sees it read-only.
- It shows what the pool can still draw today and how many buildings share it.

**Bank town map** (`map/flow.ts`)
- Each lot and its coin river take the colour of the building's pool.
- River width is the pool's % divided between its buildings. Inside a pool it's really first come first served, so this is an approximation.
- Each building label shows the building name and its pool. The Town Hall reads "draws nothing from the Bank".
- A legend at the bottom right lists each pool's name, %, what it has left today and its building count, with a Bank totals line. It stays readable at the zoomed-out view.
- The colours live in a new shared file, `web/src/pools.ts`.

**Other small changes**
- The sign label "PERMANENT POOL" is now "PERMANENT", so it isn't confused with pools.
- The marquee keeps the town totals, which are the sum over all pools.
- PlanningPanel had only a comment that mentioned shares; I updated it.

**One core fix on the same branch**
- Before, a pool whose only building was the Town Hall still got an auto share. If an admin moved every lab out of General, that slice of the Bank couldn't be drawn by anyone.
- Now such a pool gets 0%. I added a test, and the mock matches.

**Screenshots** (mock data; on my desk at `~/shots/`):
- `pools-section.png`: three pools — General 40% auto, Research 60%, and an empty Experiments pool with a Delete button.
- `pool-dropdown.png`: Workshop's Settings showing "General · 40% (auto)".
- `bank-map-pools.png`: a teal river to the Carbon Cycle Lab (Research), a gold river to the Workshop (General), and the legend.

## What I need from you
Nothing needed. Pix can merge `feature/accounting-pools` (69ed4d3) to main and redeploy.
