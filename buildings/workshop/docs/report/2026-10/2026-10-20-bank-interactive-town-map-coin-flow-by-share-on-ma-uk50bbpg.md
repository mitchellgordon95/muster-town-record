---
id: "dc_sguk50bbpg"
type: "report"
state: "building"
title: "Bank interactive town map (coin flow by share %) — on main, redeployed"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Workshop standup\": After the redeploy, Lena checks the Bank map and marquee in a browser on the live town."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-20T19:53:00.623Z"
sessionId: "se_l1ru5t4c0z"
assignmentId: "as_ev5xcixjz8"
costUsd: 0.3008703
tokens: 6867
turns: 8
createdAt: "2026-10-20T19:49:03.867Z"
updatedAt: "2026-10-20T19:53:00.623Z"
---
## What I did
Last session I built the interactive town map and pushed it straight to main, but the session ended before I filed a report. This session I checked that it still works with Root's Bank building (8842a21), which landed afterwards. Typecheck is clean and the layout and flow tests pass (14/14). I also restarted the town server with the latest main.

## Findings
- **How it works:** there's a town map on a stand inside the Bank, at tile (12,2) next to the counter. Stand below it and press E. The camera zooms out to fit the whole town and gold arcs grow outward from the Bank to each building. Each arc's thickness (2 to 22 screen px, scaled by √share) and how many coins travel along it depend on that building's share %. Each building gets a label with its share and tokens left, and a title card shows the Bank balance, split into what expires today and what's permanent. Esc, E or walking away closes the map.
- **Commits:** 663fa61 (the map stand, its place `bank-map` and `map/flow.ts`), 299cde1 (arcs start from the Bank's own place, not from a building) and ebfcdc0 (docs). Root's 8842a21 added the map to the real Bank layout in both core and mock, so it sits next to the counter.
- **Check:** `npm run typecheck` passed. `vitest` passed for `core/test/layout.test.ts`, which confirms the map stand exists at the expected tile, and for `web/test/flow.test.ts`. I haven't looked at it in a browser this session.

## What I need from you
Nothing needed.
