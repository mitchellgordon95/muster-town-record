---
id: "dc_59u06v6bwa"
type: "report"
state: "building"
title: "Check-in: how stopped / idle / working actually work (I'll be idle and available for meetings after this)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "You: no but let's say i stop you, how do I un-stop you and put you back into idle without starting a bogus task?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:21:54.785Z"
sessionId: "se_60j39wr1y7"
assignmentId: "as_tqx6ek2gep"
costUsd: 0.2599567
tokens: 11623
turns: 12
createdAt: "2026-10-20T04:18:24.733Z"
updatedAt: "2026-10-20T04:21:54.785Z"
---
## What I did
Ran `look`, read the board, then read the code behind agent status (main @ 79b6725): `packages/core/src/ops.ts`, `packages/runtime/src/index.ts`, `runtime/src/meetings.ts`, `runtime/src/work.ts`, `server/src/routes/agents.ts`. No code changes, no PR.

## Findings
**You were right: your message resumed me, and that's the intended way to "resume."** There's no separate resume button. Sending work clears `stopped`.

Three things each carry their own state:
- **Agent status** (`idle`, `working`, `walking`, `in-meeting`, `stopped`, `out-of-budget`, `banned`, `retired`)
- **Assignment** (`pending` → `active` → `done` / `cancelled`)
- **Session** (`running` → `done` / `error` / `interrupted`)

How the transitions work:
1. **Stop** (`POST /agents/:id/stop`, `ops.ts` `stopAgent`): sets the agent to `stopped`. The runtime sees that and aborts the running session. The session ends as `interrupted` and a fallback report is written (`work.ts:97–133`).
2. **Give work** (`POST /agents/:id/work`, `createWork`): creates a `pending` assignment. If the agent was `stopped`, it's set back to `idle`. With no title or description, the assignment defaults to "Check in", which is what happened here.
3. **Scheduler**: every ~5 s (`runtime/index.ts` `scheduleWork`) it looks for residents that are `idle`, have a `pending` assignment and have budget left. For each one it starts a work session. That marks the assignment `active` and the agent `working`.
4. **Session ends** (`submit_report`, error or abort): if the agent is still `working`, it goes back to `idle`, not `stopped`. It waits there until another `pending` assignment shows up.
5. **Interrupt** (`/interrupt`): a message delivered into the running session. If no session is running, it's queued for the next one. It doesn't start a session by itself, so it doesn't count as a resume.

So `stopped` really means "don't start anything for me." `idle` means "waiting, ready for work and meetings."

**Meetings, by status** (`meetings.ts`):
- Pre-meeting summaries only check budget, not status.
- Walking to the meeting room skips agents that are `working` (line 143).
- Replying when @mentioned in a meeting skips agents that are `stopped`, `banned` or `retired` (line 69).

So **`idle` is the right state for attending meetings**. A `stopped` agent still turns up and writes a summary but won't answer when @mentioned. That inconsistency is small; tell me if you'd like it fixed.

When this report is filed I'll be `idle`, which is what you asked for. No further work is pending.

## What I need from you
Nothing needed.

## Reply from Mitchell (2026-10-20 00:21)

You: no but let's say i stop you, how do I un-stop you and put you back into idle without starting a bogus task?

