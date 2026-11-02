---
id: "dc_chw7ofjl7l"
type: "report"
state: "building"
title: "Planner desks now follow the building's size, and number boxes can be emptied (0ff2338, redeploy requested)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Pix\": Objectives and KPIs (no North Star): each building goal gets 2 or 3 objectives (one sentence, quarter horizon); key results hang off an objective (2 to 4 each),"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T06:06:35.187Z"
sessionId: "se_soie2djxnf"
assignmentId: "as_toekad4g3t"
costUsd: 0.6208242000000002
tokens: 25511
turns: 18
createdAt: "2026-10-27T05:53:00.444Z"
updatedAt: "2026-10-27T06:06:35.187Z"
---
## What I did
Pushed 0ff2338 straight to main and requested a redeploy. Typecheck passes and the web tests pass (73/73), including a new test, test/desksFor.test.ts.

## Findings
- **Desks follow the building's size.** When you draw or resize the new building in the planner, its Desks number is now set to the most desks that fit (`desksFor` in packages/web/src/map/townPlan.ts, which uses the same `labSize` rule as the server, capped at 24). Moving the building keeps whatever count you typed. Typing a bigger number still grows the building to fit. A building too small for even one desk keeps its last count and grows to fit when you let go.
- **The stuck zero is gone.** The new `NumberInput` in panels/ui.tsx keeps what you type as text, so you can clear the box and type a new number. Every valid number is applied (kept between the box's min and max), and the box shows the real value again when you click away. It's now used for the Desks boxes in the planner toolbar, the Planning desk and the Building panel, and for "Max turns / session".
- **Not changed:** resizing an existing building in the planner doesn't change its desk count, because saving the plan only sends the building positions and sizes.
- **Not checked live:** opening the planner needs a signed-in human with permission to manage buildings, and desks can't sign in. The mock UI hides the planner too. 0ff2338 should be live after the restart.

## What I need from you
Mitchell: once 0ff2338 is live, open Plan the town, draw a building, and check two things: Desks changes as you drag its walls, and you can clear the Desks box to type a new number.
