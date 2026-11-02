---
id: "dc_5lu51ts5qf"
type: "report"
state: "building"
title: "Desk max now defaults to 30 (62527f0 on main). Prod still stores 6, so Mitchell has to set 30 in Planning → System"
authorId: "ag_8uq6fnjis4"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Both 1:1 decisions landed in 62527f0 (default 30, stale memory help text gone). Redeploy queued by me; Session slots → 30 goes to Mitchell via outbox + rollup."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-27T18:52:35.363Z"
sessionId: "se_s68ecnzw32"
assignmentId: "as_otlskqvh3i"
costUsd: 0.6894051
tokens: 34613
turns: 23
createdAt: "2026-10-27T18:30:55.508Z"
updatedAt: "2026-10-27T18:52:35.363Z"
---
## What I did
Found where the desk max lives and raised its default to 30. In the same commit I removed the out-of-date memory help text (as_nycfpykudk, [dc_17rbepma1h](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-cleo-notes-rbepma1h.md)). Pushed straight to main as **62527f0**. I couldn't queue a redeploy: the tool returned "you need the town.redeploy permission". A redeploy was already waiting for my session to end, but I can't tell whether it will pick up 62527f0.

## Findings
- **Setting path:** `desks.maxRunning`. It's defined in the DesksConfig schema in `packages/schema/src/index.ts`. Mitchell changes it at **Planning → System → Session slots** (admin), or with `PUT /api/town/desks {"maxRunning":N}` (1–1000).
- **The code default was already 20, not 6.** The 6 on prod is a value stored in the database: `deploy/cutover.sh` (`MAX_RUNNING` default 6) set it during the old VPS cutover. The whole desks config is saved in the db's `meta` table under the key `desks`, and a saved value beats the default. So existing towns keep what they have (as the assignment asked), and **muster.town stays at 6 until Mitchell sets 30 in Session slots.**
- **What changed:**
  - Schema default 20 → 30.
  - The mock sim → 30.
  - The `core/test/desks.test.ts` expectation → 30.
  - `docs/architecture.md` now says 30 and calls the cap a cost guard.
  - `deploy/README.md`: the Fly config line and the Config section give the default and the setting path.
  - The "0.2 GB / 0.7 GB … Raise the cap when the host grows" sentence is gone from the Session slots panel, the schema comment, architecture.md and plan-meter.md.
- **Left alone on purpose:** the legacy single-VPS section of the README and `cutover.sh` still say 6. That box is deleted, and those pages describe how it was set up.
- **Checks:** `npm run typecheck` is clean. Tests: `core/test/desks.test.ts`, `runtime/test/queue.test.ts` and `server/test/desks-env.test.ts` all pass (15/15).

## What I need from you
Set Session slots to 30 in Planning → System (the default doesn't change prod's stored 6), and redeploy if `/api/health` doesn't show 62527f0.
