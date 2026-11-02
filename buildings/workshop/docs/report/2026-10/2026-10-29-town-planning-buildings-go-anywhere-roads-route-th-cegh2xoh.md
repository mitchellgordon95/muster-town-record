---
id: "dc_j0cegh2xoh"
type: "report"
state: "building"
title: "Town planning: buildings go anywhere, roads route themselves (d32bace on main, PR #83); live check parked"
authorId: "ag_7q860fxskw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation already ran as as_r2nr9jakxc (dc_l6te0d558y): d32bace live, roads unchanged. Door-side follow-up (furniture.ts) noted, not assigned: Mitchell's flag did not ask for it."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T20:20:27.672Z"
sessionId: "se_m3gjscalgq"
assignmentId: "as_sdhj7fvvhe"
costUsd: 3.9173398000000015
tokens: 195867
turns: 86
createdAt: "2026-10-29T20:12:47.187Z"
updatedAt: "2026-10-29T20:20:27.672Z"
---
## What I did
Built Mitchell's flag [dc_sepd0hq0it](../../flag/2026-10/2026-10-29-i-d-like-to-be-able-to-place-a-building-anywhere-a-pd0hq0it.md) in one step. Roads are now a layer worked out from the building lots, and the "north/south of the road with a straight path" rule is gone. Merged PR https://github.com/mitchellgordon95/muster-town/pull/83 as **d32bace** (CI green, `npm run check` green) and queued a redeploy. The live check is parked on that deploy. Topic page: [dc_79y2l31lef](../../wiki/2026-10/2026-10-29-town-planning-free-placement-and-derived-roads-y2l31lef.md).

## Findings
- **Rule now:** a building can stand on any free grass on the map. These rules stay: whole tiles, the minimum size for its desks, at most 48×38, on the map, not on the two trunk-road rows, and one tile of grass between buildings and around the Bank. The only road rule left is that every door must reach a road. If one can't, the plan check says "no road can reach its door (it's boxed in)".
- **Roads are worked out from the lots, so nothing is stored and no migration is needed.** `deriveRoads` in core/world/road.ts lays the trunk road first. Then, for each building and the Bank, a grid router runs a road from the door to the nearest road tile:
  - it never enters a lot;
  - a turn costs 4 steps, so roads run in long straight lines;
  - doors nearest the trunk are routed first, so farther buildings join their roads;
  - the same lots always give the same roads.
- **The map and walking:** `computeLayout` draws the roads. The planner's dry run returns that same grid, so the roads redraw live while you drag. Roads are ordinary path tiles and grass was already walkable, so walking needed no change.
- **Live town unchanged:** I took the live lots from GET /api/town and ran them through the new code. They pass the plan check, and the road tiles match the live grid exactly. Nothing changes on the live map until someone moves a building.
- **Tests (core/test/plan.test.ts):** every door reaches the trunk walking only on road tiles; no road tile is inside a lot or the Bank; a lab boxed in behind another routes around it; a building far from the trunk passes the check; the seeded labs keep their straight roads; a boxed-in door is reported.
- **Local check on the real server** (dev mode, admin): I placed Kelp Lab north of the Workshop, Far Field far to the north-east and South Hollow far to the south. Each got a road; Kelp Lab's goes down and then around the Workshop. A dry run that moved Far Field to the top-left joined its road onto Kelp Lab's. Picture (taken from that local run, not the live town):
  ![Town planning: Kelp Lab and Far Field placed off the road, each with a derived road](/api/media/mf_hjk5k2e5k2.png)
- **Differences from the brief:**
  - The door does not switch to whichever side the router leaves from. It stays bottom middle north of the trunk and top middle south of it, and the router starts from there. Moving it would mean the room's furniture layout has to know which side the door is on, which needs a change in furniture.ts that I didn't make.
  - Mock mode can't plan at all (its plan preview returns 501), so instead of the mock-mode check I ran the real server locally.
  - The live check can't take the off-road picture: only a real admin can run a planning dry run, and a guest gets 401.

## What I need from you
Nothing needed.
