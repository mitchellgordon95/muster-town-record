---
id: "dc_7g0v7qai7v"
type: "note"
state: "building"
title: "Exploration 2026-11-20: a captain can't decide most asks in their own subtree"
authorId: "ag_g97rq6gyux"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["exploration","captain","asks"]
createdAt: "2026-11-20T00:01:50.014Z"
updatedAt: "2026-11-20T00:01:50.014Z"
---
Pix 1, exploration as_5di6z5wxyu, read on main 8b962281 (= live /api/health commit at 2026-11-20T00:00:17Z).

## What the code says
- **Grants and retainers accept the captain.** `GrantDesk.canFund` (packages/core/src/grants.ts ~L970) = `building.fund` on the building OR `goalTree.owns(actor, g.goalId)`. `canDecideRetainer` (retainers.ts L142) is the same. Captain requests and goal proposals also check the captain.
- **Every other ask does not.** `requireDecider` (packages/core/src/asks.ts L281) = human AND `permissions.can(actor, "building.fund", a.buildingId)`. No captain clause. That gates `POST /api/asks/:id/decide`, which the ask card uses for every branch whose kind is "ask": click, policy, credential, do, meeting, keyResult and rule asks, and any ask with no target.
- **The in-tray routes don't cover asks.** `intrayRoutes` (packages/core/src/intray-routes.ts) builds routes for grants, stopped grants, goal proposals, captain requests, retainers and reports, keyed by those ids. An ask is looked up by `routes[a.targetId ?? ""]`.
  - So on the ask card, `canDecide` is `undefined` for an untargeted ask, and `AskCard` shows the buttons when `canDecide !== false` (AskCard.tsx L171). A non-admin captain presses one and gets 403 building.fund.
  - And `mineAsks` (web queueOrder.ts L46) keeps an ask when it has no route (`!r || r.mine`). A captain's default "Mine" view (intrayRoutes `defaultView`) therefore lists every untargeted ask in the whole town, not only their subtree's.
- `askGoalId(world, a)` (asks.ts L788, from PR #527) already resolves any ask to its goal: target grant, retainer's grant, captain request or proposal goal, else the building's attachment. That is the route an ask needs.
- No test covers a captain deciding an ask: no test that calls `decideAsk` mentions a captain.

## Live state
- Every goal in the live tree (GET /api/goals) is captained by Mitchell. No second human has ever steered a subtree on the live town. The captain-rights grant gr_zsm1piyqyx ([dc_ooe47kx4un](../../wiki/2026-11/2026-11-01-captain-steering-rights-e47kx4un.md)) closed on test evidence only: "no second human account for a live check". A test account exists now (dungeonrpg99-ops, skill [dc_11e758uhzj](../../../../../library/skill/2026-11/2026-11-06-test-account-live-check-e758uhzj.md)).
- 0 open asks at 00:00Z, so nobody is hurt today. The gap shows up the first time a stranger captains a goal, which is this goal's own promise.

## What I infer
The building goal says a human can own a piece of the tree and steer it "through goals, grants, report review and meetings". The decision queue is now the main steering surface (asks replaced rollups). For a captain who is not an admin, money asks work, but the rest of their queue is noise from other subtrees with buttons that fail.

## What I don't know
- Whether `POST /api/requests/...` (request asks, "do") checks a captain; not read.
- How many untargeted asks a week the town files; the events API's default window held no ask events.
