---
id: "dc_rcwe8crdb4"
type: "report"
state: "building"
title: "PR #422: the Secretary becomes the Town Hall's manager (parked on CI)"
authorId: "ag_ey0umg51ch"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The continuation as_50m3fvdb5t waits on PR #422's CI, merges on green and checks the Town Hall's manager live. The open question (should managerAgentOf count the Secretary, which decides who works the Town Hall in-tray) goes to Mitchell in rollup 56, not to code."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T21:09:33.210Z"
sessionId: "se_wxqxt3qgqy"
assignmentId: "as_tjwtuf45sr"
costUsd: 1.4714729999999998
tokens: 73574
turns: 37
createdAt: "2026-11-10T21:09:11.850Z"
updatedAt: "2026-11-10T21:09:33.210Z"
---
## What I did
My desk has no admin bearer: AGENT_TOWN_TOKEN and MUSTER_TOWN_TOKEN are agent tokens, and /api/me refuses them. So the one-call PATCH was out. I opened draft PR #422 instead (https://github.com/mitchellgordon95/muster-town/pull/422).

A migration alone would not have held. `Reorgs.ensurePlanner()` → `seatAsManager` writes the Planner back into town-hall.managerAgentId on every call: seed, Planner runs, Town Hall 1:1s and reorgs. Its source is goal-changes.ts:81-84. It would undo a migration within minutes.

The PR changes three things:
- **`Secretary.ensure()`** now seats the Secretary as town-hall `managerAgentId` and calls `syncManagerRoles`. It runs at every boot (server main.ts:66), so every World gets it, hosted ones included. No migration was needed.
- **`syncManagerRoles`** grants the town-hall manager role only when the manager is the Secretary. A Planner seated there still gets no role.
- **`seatAsManager`** in `ensurePlanner` no longer overwrites a live Secretary.

Tests: core 909/909 and server 304/304 on my desk. secretary.test.ts has a new case, and its old assertion "Planner stays manager" is flipped.

## Findings
Live state at 20:57Z: GET /api/buildings/town-hall shows managerAgentId = ag_lywy3igvel (the Planner). That stays true until #422 merges and deploys.

**What the Secretary can do once #422 is live:**
- It gets `building.assign` on town-hall. The 20:52Z refusals go away.
- `assign` works when it names its own id, `agentId: ag_7tiwyqva83`. That puts the work on its own queue (domain.ts:66).
- `assign` with agentId left out still fails with "no manager agent to fork". The reason is that `managerAgentOf` excludes the Town Hall.
- `schedule` works with `takerId` = the Secretary (schedules.ts:98).
- The Planner's schedules sc_8zoclbtrwp and sc_m9g7axmnoy are untouched. They belong to the building.

**Paths that special-case kind 'town-hall', after #422:**
- **domain.ts:319, `managerAgentOf`** returns nothing for the Town Hall, and I left it that way. Without it the Town Hall in-tray would become the Secretary's to work. As it is, the in-tray stays the humans' (`intrayWorker` = human), the Secretary has no forks and the hydrant is unchanged.
- **permissions.ts:126, `managesABuilding`** only gates `town.redeploy`, so the Secretary gets no redeploy right. That is fine.
- **grants.ts:1035, `requireWriter`**: the Secretary can't write key results on Town Hall grants. There are none today.
- **prompts.ts:160**: the Secretary gets no manager memory or grants block in its session. Its own run prompts are unchanged.
- **New rights from the manager role:**
  - `building.review` on town-hall lets it `review` docs filed at the Town Hall and facilitate town-wide meetings (meetings.ts:98).
  - `building.manage` lets it change the Town Hall's settings.
  - `building.fund` is never an agent's (permissions.ts:69), so it still decides no ask.

**What remains of gr_94vogc1ztq step 2:** resident publish. A resident's `write` with state building must land in its building's filing cabinet (verbs/docs.ts:218). Also open: whether `managerAgentOf` should count the Secretary. That would make `assign` with no agentId work, and change who works the Town Hall in-tray. It needs Mitchell's call.

## What I need from you
Nothing needed. I resume on #422's CI, merge it on green, then check it live.
