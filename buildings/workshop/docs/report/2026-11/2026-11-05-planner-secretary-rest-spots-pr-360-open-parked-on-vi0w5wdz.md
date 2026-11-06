---
id: "dc_buvi0w5wdz"
type: "report"
state: "building"
title: "Planner/Secretary rest spots: PR #360 open, parked on CI"
authorId: "ag_3j3km4us4o"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #360 parked on CI; its continuation as_z81jwmzsad (waiting on {pr: 360}) merges it and takes the screenshot. Will fold into rollup 49 once the four PRs (#357-#360) are live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:29:13.238Z"
sessionId: "se_n1o76fsq3o"
assignmentId: "as_aa1d98mxv8"
costUsd: 0.9923006999999998
tokens: 49615
turns: 19
createdAt: "2026-11-05T19:28:33.370Z"
updatedAt: "2026-11-05T19:29:13.238Z"
---
## What I did
Opened draft PR #360 (https://github.com/mitchellgordon95/muster-town/pull/360) for piece 2 of 3 of flag [dc_r7u6bkaei4](../../flag/2026-11/2026-11-05-user-stats-panel-in-the-workshop-should-show-stats-u6bkaei4.md). When idle, the Planner now stands next to the goal-tree chart and the Secretary next to the Town Hall in-tray. Tests pass locally: core 777, server 294, runtime 232, plus typecheck. I'm parked until CI finishes.

## Findings
- **Change:** `computeLayout` (packages/core/src/world/layout.ts) takes a `rests` map built in `map.ts` `compute()`. It holds non-fork Town Hall residents whose title is in `TOWN_HALL_RESTS` = {Planner: goal-tree, Secretary: intray}.
- **Where their desks are drawn:** each one's desk place `desk:<id>` goes on the first walkable tile right, left, below or above the piece's stand. That tile must not be another stand, the door or the other rest spot. In the default layout that is (13,1) beside the goal tree and (15,8) beside the in-tray, relative to the lot. If no such tile exists, the stand itself is used.
- **Desk bookkeeping is unchanged:** both still hold mod-station desk slots, and free seats and other residents stay at the mod station. Everything that reads `deskOf().pos` (walkHome / walkIdleHome, walkToDesk, creation) now sends them to the new spot. Sessions and meetings can still walk them anywhere.
- **Live bodies:** on deploy, the rebuild moves the desk place, and the idle tick walks them there.
- **Tests:** packages/core/test/town-hall-rests.test.ts (3 tests).
- **Docs:** one line updated in docs/architecture.md.
- **Next session:** if CI is green, merge #360 without a redeploy. Then park on {deploy: merge sha}, open https://muster.town/ Town Hall, and take a cropped screenshot showing the Planner by the goal tree and the Secretary by the in-tray. If CI is red, fix it.

## What I need from you
Nothing needed.
