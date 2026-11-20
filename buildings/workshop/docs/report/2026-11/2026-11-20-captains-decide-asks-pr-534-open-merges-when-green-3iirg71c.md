---
id: "dc_r93iirg71c"
type: "report"
state: "building"
title: "Captains decide asks: PR #534 open, merges when green"
authorId: "ag_antubbo3nz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T02:02:16.710Z"
sessionId: "se_9bv6xodw3o"
assignmentId: "as_vz5hciiesr"
costUsd: 1.9064630000000002
tokens: 95323
turns: 44
createdAt: "2026-11-20T02:02:16.696Z"
updatedAt: "2026-11-20T02:02:16.710Z"
---
## What I did
Wrote the captain rule for asks in core, routed every live ask by its own id in the in-tray, and changed the web to read an ask's route by ask id. Added tests and updated docs/invariants/asks.md invariant 5. Opened PR #534 (https://github.com/mitchellgordon95/muster-town/pull/534), parked to merge when green.

## Findings
- **Core** (`packages/core/src/asks.ts`): the new `canDecideAsk(world, actor, ask)` lets a human decide when they have `building.fund` on the ask's building OR `goalTree.owns(actor, askGoalId(world, ask))`. For a goal-proposal ask the rule is `canEdit` at the proposal's node. `requireDecider` uses it, so `decideAsk` and `deferAsk` give a 403 to everyone else. It is exported from the core index.
- **Routing** (`packages/core/src/intray-routes.ts`): `intrayRoutes` takes `items.asks` (the Town Hall intray already carries `asks`). It adds one route per ask, keyed by ask id: the goal is `askGoalId` and the owner comes from `ownerOf`, so `mine` is true only for the nearest captain. `canDecide` comes from `canDecideAsk`.
- **Web**: the new `askRoute(ask, routes)` in `queueOrder.ts` looks up routes[ask.id], then the target, then the source doc. `mineAsks` uses it. In DecisionQueue, AskCard's `canDecide` uses it. FundingView now gets `routes`, so its cards also hide the buttons and show "A captain or admin decides this."
- **Tests, all run on the desk:**
  - `packages/core/test/captain-asks.test.ts` (3 tests): a leaf captain decides and defers inside the subtree and gets 403 outside. A plain member, an agent and an anonymous viewer cannot. An admin can everywhere. Routes are checked too.
  - The server test in `packages/server/test/asks.test.ts`: a non-admin captain of a leaf goal gets 200 deciding a click ask from LAB. The captain gets 403 on an ask from a second building attached outside the goal. The in-tray route shows mine and canDecide true inside and false outside, and defaultView is "mine".
  - Web `decisionQueue.test.tsx`: the ask's own route wins over its target's route.
  - Results: `npm run typecheck` passed, and core+web passed 1554 tests. Server passed 361 tests, and `npm run check --fast` was green.
- **Key results:** kr_myfc0qi5j5 is met on code once #534 is merged and live. I am not claiming it until the live check. kr_lgft8zxocd and kr_wrh4pcxhpk need step 2: the test account captaining a leaf goal on the live town.

## What I need from you
Nothing needed.
