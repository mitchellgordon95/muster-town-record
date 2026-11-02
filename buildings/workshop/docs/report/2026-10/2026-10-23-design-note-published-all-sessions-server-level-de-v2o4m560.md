---
id: "dc_eiv2o4m560"
type: "report"
state: "building"
title: "Design note published: all sessions server-level, desks on demand (dc_e8tgzb2t3b)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-24T19:01:04.955Z"
sessionId: "se_51xvnodsap"
assignmentId: "as_8iert3cp72"
costUsd: 0.9239852
tokens: 35160
turns: 23
createdAt: "2026-10-23T04:31:08.448Z"
updatedAt: "2026-10-24T19:01:04.955Z"
---
## What I did
I read the runtime on main at 34cc56c: `session.ts`, `work.ts`, `meetings.ts`, `chat.ts`, `desk/*`, `HostHooks` and the desk workspace code. From that I wrote the design note [Design note: all sessions run server-level, desks on demand](../../article/2026-10/2026-10-23-design-note-all-sessions-run-server-level-desks-on-tgzb2t3b.md) and filed it in the building. The repo is unchanged, so I made no commit and no redeploy.

## Findings
- **Today:**
  - Host work sessions get the town verbs plus WebSearch/WebFetch. They have no shell or file tools, and they refuse any building with code access. That is why all Workshop work runs in desks.
  - The facilitator gets the town verbs only.
  - Meeting replies, summaries and chat are single model calls with no tools. That's why the standup felt fast, and it corrects what Pix said there.
- **Desk toolset:** four new verbs, backed by the runtime the same way redeploy is:
  - `desk_start` runs a new `agent-town-desk prepare` that only sets up the checkout.
  - `desk_run` runs a command in the background and returns the last 16 KB of output.
  - `desk_output` pages through a long run, reusing Fly's existing log/exit polling.
  - `desk_stop` also runs automatically when the session ends.
  - No model keys go into the desk, and I left out remote file read/write/edit on purpose.
- **Delegation:** a new `delegate` verb creates a desk assignment for the agent itself. A work session then parks on it with the existing `submit_report resumeWhen {assignment}`. A 1:1 just puts the assignment in the queue.
- **Runtime changes:**
  - The backend is chosen per assignment (`assignment.desk` column plus a migration), not per building.
  - The Fly/docker exec splits into start + poll.
  - Open desks are tied to the host session.
  - `maxRunning` splits into a session limit and a desk limit.
  - The host system prompt for code buildings gets a short block about the new tools.
  - Unchanged: funding, the report flow, how desks publish over `/mcp`.
- **Known gap:** we don't record what Fly bills for Machine time, for desk sessions today or for the new tools.
- I pointed Sage at the note because of the 1:1 escalation question.

## What I need from you
Mitchell: answer the 4 questions at the end of [dc_e8tgzb2t3b](../../article/2026-10/2026-10-23-design-note-all-sessions-run-server-level-desks-on-tgzb2t3b.md). The main one is whether code buildings keep desk assignments as the default for now (my recommendation) or switch to server-first immediately.
