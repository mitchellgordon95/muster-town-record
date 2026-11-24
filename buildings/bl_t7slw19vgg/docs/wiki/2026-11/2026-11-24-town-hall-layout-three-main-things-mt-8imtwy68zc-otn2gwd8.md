---
id: "dc_3cotn2gwd8"
type: "wiki"
state: "building"
title: "Town Hall layout: three main things (mt_8imtwy68zc)"
authorId: "ag_5gfsp57fhl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-24T22:09:35.313Z"
updatedAt: "2026-11-24T22:09:35.313Z"
---
Mitchell, 1:1 mt_8imtwy68zc decision 2 (2026-11-24): the hydrant, the goal tree planner and the meeting desk are the Town Hall's three main things. The town organization board moves outside. The library becomes a tiny thing in a corner. Everything else is less prominent. Assignment as_i4k4591tky (Teo 2).

**Read as:** "town organization board" = the 5x2 town map table (it opens town planning, where buildings go). The Town Hall board (town-wide FYIs) stays inside, smaller and off-centre. If Mitchell meant the FYI board, swap that in a follow-up.

**PR #594** (draft, parked to merge when green). Live once /api/health's commit contains it:
- core `world/furniture.ts` Town Hall pieces: goal tree `row(3, GOAL_CHART)` at (7,0), opposite the door (8,10), plants at (6,1) and (10,1). Hydrant at (4,5), meeting table at (10..13,5), on one row. The Secretary rests at hydrant +(-2,-1). Library is one SHELF at (1,1) and the manual a BOOK at (2,1). Board at (3,0), stats at (15,1), schedule at (15,5). Mod station, bench, planning desk and help sign are unchanged.
- The town map is outside: `TILE.TOWN_MAP` is now a 1-tile board, place `town-map` with buildingId null. In the fountain map (square.ts) it sits at doorX+3, mirroring the bulletin board at doorX-3. Other shapes use `bulletinSpot(..., dx=3)` in layout.ts.
- web: `sprites.ts` `goalChartArt` (a 3-tile sheet) and `drawTownMapBoard`; `world.ts` draws them. `helpCard.ts` HALL_ORDER lists hydrant, goal tree and meeting table first, so they are tour hotspots 1-3. `mock/layout.ts` mirrors all of this.
- Tests: core 1,163 passed and web 500 passed on the desk. furniture.test.ts has a new test that pins the layout.

**Screenshots (desk cache):** ~/shots/hall/before.png and after.png. To make them: `VITE_MOCK=1 npx vite --port 5199` in packages/web, then `node ~/scratch/pw/hall.mjs TAG`. That opens the Town Hall help tour (`__muster.open({kind:"help", id:"bl_townhall"})`).
