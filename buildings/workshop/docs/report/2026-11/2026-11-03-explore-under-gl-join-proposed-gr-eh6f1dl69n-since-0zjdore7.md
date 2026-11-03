---
id: "dc_ex0zjdore7"
type: "report"
state: "building"
title: "Explore under gl_join: proposed gr_eh6f1dl69n, \"since you last reviewed\" for returning captains"
authorId: "ag_0fxsp6r75j"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_w97icr6obz","gr_eh6f1dl69n"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done: gr_eh6f1dl69n (\"since you last reviewed\" for returning captains, 350,000) is in the Town Hall in-tray on its own row; nothing to queue until a human decides it. Folds into rollup 39."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T02:56:27.674Z"
sessionId: "se_5unjoxk73i"
assignmentId: "as_okxkncoucv"
costUsd: 0.7109399
tokens: 35547
turns: 17
createdAt: "2026-11-03T02:55:05.153Z"
updatedAt: "2026-11-03T02:56:27.674Z"
---
## What I did
I checked the leftover ideas against the code on main (335c586). Town blockers already ran through 7 editions, and the deck already exists. I then looked for steering gaps that the four funded grants under gl_join don't cover. I wrote the findings to [dc_w97icr6obz](../../note/2026-11/2026-11-03-findings-a-returning-captain-has-no-since-you-last-7icr6obz.md) and filed one proposal, gr_eh6f1dl69n (350,000 tokens).

## Findings
- docs/goals.md step 4 still lists "the per-user review marker (`lastReviewedAt` per human, "decided by Lena")" as left for later. Nothing in packages/*/src implements it.
- docs/goals.md promises that Planner's brief carries "an event digest since the human's last review". `Reorgs.plannerBrief` has no digest, because no review time is stored.
- Slide 1 of the deck (`townSlide`, core review-deck.ts) is the same whole-town view for everyone. It isn't scoped to the viewer's subtree and has no "since" window. Agents already get `Presence.digest` for their offline window; humans get nothing like it.
- The proposal: a nullable users.lastReviewedAt column, a core `sinceDigest` over an allow-list of events routed with Goals.route that names who did each thing, a "Since you last reviewed" block on slide 1 and in the in-tray header, the same digest in Planner's brief, and tests. It has 3 key results, due 2026-11-08 and 2026-11-09. The town's estimate for similar grants: 290k–698k tokens spent.

## What I need from you
Nothing needed.
