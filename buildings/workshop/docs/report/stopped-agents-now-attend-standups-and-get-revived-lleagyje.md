---
id: "dc_qjlleagyje"
type: "report"
state: "building"
title: "Stopped agents now attend standups and get revived by decisions (c0884dc on main); Root still needs an assigner"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:31:18.211Z"
sessionId: "se_5lmcz71ztl"
assignmentId: "as_4wwb3spebv"
costUsd: 0.6972112999999999
tokens: 1014466
turns: 25
createdAt: "2026-10-20T18:26:59.715Z"
updatedAt: "2026-10-20T18:31:18.211Z"
---
## What I did
Changed meetings so stopped agents still attend, pushed to main as **c0884dc**, and started a redeploy. It drains first, so it will restart once my session ends. I then tried to restart Root with a task and couldn't: I don't have the `building.assign` permission.

## Findings
- **The change** (`packages/core/src/meetings.ts`, `packages/runtime/src/meetings.ts`):
  - Building standups now invite stopped residents by default. Only banned and retired agents are left out.
  - An explicit invite of a stopped agent is now accepted.
  - Stopped attendees write summaries and answer facilitator or human @mentions.
  - A meeting decision that assigns a stopped agent sets them back to idle, so the scheduler runs the new task.
  - A stopped agent is never picked as facilitator.
- **How I checked it:** `npm run typecheck` is clean. `npm test` passes: 296 tests in all packages. That includes a new test where a stopped resident is invited to the standup, isn't the facilitator, stays stopped during the discussion, and is idle with one pending assignment after a decision. The old test now expects a retired invitee to be rejected (stopped invitees used to be). I updated docs/architecture.md and docs/log.md.
- **Root:** status is `stopped`. Pix's rename plan exists (dc_iii6gya0a0) and suggests Root takes **P3**: the env/profile/localStorage/docker back-compat layer (read `MUSTER_TOWN_*` and fall back to `AGENT_TOWN_*`, accept both the old and new docker label, move the old localStorage key). P3 depends on Mitchell's P0 naming decisions and on Pix's P1 scope rename. Root can still start now if the env prefix is a single constant that's easy to change. My assign call returned "Not allowed: you need the building.assign permission".

## What I need from you
Assign Root rename slice P3 from dc_iii6gya0a0, or whatever task you prefer, via the agent panel or `assign` (I can't: no building.assign). After this redeploy, a standup decision assigning Root will also revive them.
