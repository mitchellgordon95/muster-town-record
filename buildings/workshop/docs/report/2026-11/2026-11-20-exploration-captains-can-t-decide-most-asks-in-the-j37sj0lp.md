---
id: "dc_myj37sj0lp"
type: "report"
state: "building"
title: "Exploration: captains can't decide most asks in their subtree; proposed gr_0vuiuqcw8p (200k)"
authorId: "ag_g97rq6gyux"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Verified the code claim: requireDecider (packages/core/src/asks.ts L281-284 at 8b96228) checks only building.fund, no captain clause. Proposal gr_0vuiuqcw8p is in the Town Hall in-tray with its card ak_15ideg0ixt (filed by Pix 1); my own diff-first wording landed as an entry on its thread. Nothing to queue until Mitchell funds, counters or rejects."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-20T00:04:06.313Z"
sessionId: "se_0ka1lkealf"
assignmentId: "as_5di6z5wxyu"
costUsd: 1.6368170999999996
tokens: 81841
turns: 30
createdAt: "2026-11-20T00:02:26.803Z"
updatedAt: "2026-11-20T00:04:06.313Z"
---
## What I did
Read the live goal tree and the code for ask deciding and in-tray routing on main 8b962281, which is the live commit. Wrote up the findings in [dc_7g0v7qai7v](../../note/2026-11/2026-11-20-exploration-2026-11-20-a-captain-can-t-decide-most-0v7qai7v.md) and proposed gr_0vuiuqcw8p: "Captains decide every ask in their subtree", 2 steps (M + S = 200k).

## Findings
- Grants, retainers, captain requests and goal proposals all let the goal's captain decide. `requireDecider` in asks.ts does not: it allows only `building.fund`. So a non-admin captain gets a 403 on every other ask kind: click, policy, credential, do, meeting and keyResult asks, plus asks with no target.
- `intrayRoutes` has no route for an ask itself. Because of that, AskCard shows the buttons (`canDecide` is undefined), and `mineAsks` keeps every untargeted ask in a captain's default "Mine" view, from the whole town.
- `askGoalId` (from PR #527) already maps any ask to its goal, so the fix is small.
- Mitchell captains every goal in the live tree, so nobody has hit this yet. There were 0 open asks at 00:00Z. The earlier captain-rights grant gr_zsm1piyqyx closed without a live check by a second human. The test account now makes that check possible, and that is step 2.

## What I need from you
Decide whether to fund gr_0vuiuqcw8p in the Town Hall in-tray.
