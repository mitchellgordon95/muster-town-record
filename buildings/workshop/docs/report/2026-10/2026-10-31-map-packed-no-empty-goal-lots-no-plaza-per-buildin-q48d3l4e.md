---
id: "dc_zcq48d3l4e"
type: "report"
state: "building"
title: "Map packed: no empty goal lots, no plaza per building (PR #168 = b4c2dc1 merged, parked on its deploy)"
authorId: "ag_2rp87f01mr"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #168 = b4c2dc1 merged (map packed from the goal tree: no empty goal lots, no plaza per building, 190×57 → 114×28). The live check already waits as as_an3mguk4zb on deploy b4c2dc1; it should also confirm branch CI on #168 went green since the merge preceded CI. Goes in rollup 35 as a Shipped item once live-checked."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T18:21:44.942Z"
sessionId: "se_50dzr1hfl3"
assignmentId: "as_8ahfilyw6j"
costUsd: 4.0090086
tokens: 200450
turns: 76
createdAt: "2026-10-31T18:21:30.530Z"
updatedAt: "2026-10-31T18:21:44.942Z"
---
## What I did
Rewrote the map layout from the goal tree in core `world/tree.ts` to make all three of Mitchell's fixes (1:1 mt_wql34b8gkl). I also updated roads, the Bank position, the marquee, the web signpost lookup, tests and docs. PR https://github.com/mitchellgordon95/muster-town/pull/168 is merged as **b4c2dc1**, and a redeploy is queued. At 18:21Z the live server was still on 88a58a4, so this session is parked on deploy b4c2dc1 for the live check.

## Findings
- **Layout rules now:**
  - Only goals with a building under them are drawn. Fund, the objectives and the other goals with no building get nothing on the map; the goal tree at the Town Hall still lists them.
  - A goal with no building of its own and only one drawn child folds into that child, so a chain of goals is one step, not a long walk.
  - **No plaza per building.** A building stands right on its parent goal's street, with one tile of grass between neighbours.
  - A goal with drawn children gets its own street one row down, joined by a one-tile drop, with a signpost beside the drop.
  - The Town Hall is at the root, above the main street. The Bank now sits under it at the west end (`BANK_LOT` x 48 → 2), and the Bank's marquee moved to the right of the Town Hall.
- **Live tree:** the map goes from 190×57 to 114×28 tiles. The labs form one row below the main street. Onboarding and UI/UX hang off the Workshop goal's street, and Prod, Bank Transparency and Code Legibility off Trust's.
- **Reachability:** on the new layout of the live tree, every door and every place can be reached from the plaza.
- **Browser check (local server seeded with the live tree):** whole-town view and street view, 0 console errors.
- **Tests:** typecheck, check:docs and knip pass. Core 533/533, server 225/225 and web 189/189 pass on the merged branch.
- I merged before CI finished; main has no required checks. Branch CI should be checked next session.
- **Before crop:** mf_wwd3c4dx9o (the live grid at 49fb455, 760×228). The after crop comes from live once b4c2dc1 is deployed.
- The topic page "Map from the tree: packed layout" ([dc_e5xzfn81ge](../../wiki/2026-10/2026-10-31-map-from-the-tree-packed-layout-xzfn81ge.md)) has the rules and the desk scripts for the check.
- Also updated: docs/goals.md, which marks the two open map questions as answered, and docs/how-work-gets-done.md, which marks the obvious fixes as built.

## What I need from you
Nothing needed.
