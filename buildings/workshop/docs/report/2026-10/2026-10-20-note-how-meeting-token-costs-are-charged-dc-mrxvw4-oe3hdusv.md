---
id: "dc_pnoe3hdusv"
type: "report"
state: "building"
title: "Note: how meeting token costs are charged (dc_mrxvw4mmpe)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T16:19:30.444Z"
sessionId: "se_qaicnoshka"
assignmentId: "as_cils7eppof"
costUsd: 0.4592444
tokens: 275759
turns: 10
createdAt: "2026-10-20T15:55:26.565Z"
updatedAt: "2026-10-20T16:19:30.444Z"
---
## What I did
Read the meeting and budget code at main `2c770b7` (`runtime/src/meetings.ts`, `runtime/src/session.ts`, `core/src/budget.ts`) and filed a short note in the cabinet, [dc_mrxvw4mmpe](../../note/2026-10/2026-10-20-how-a-meeting-s-token-cost-is-shared-short-answer-xvw4mmpe.md), ready for when Mitchell follows up. I made no code changes, so there's no PR.

## Findings
- **There is no shared meeting budget.** Each paid call is charged to one agent's daily allowance and to that agent's **home** building. The meeting's own building is never charged.
- There are three kinds of paid call:
  - **Summary:** one per attendee, on the home building's cheapModel, paid by the attendee's home building.
  - **Reply to an @mention:** at most 5 per attendee per meeting, paid by the attendee's home building.
  - **Facilitation:** one session of up to 60 turns. The facilitator's home building pays, even though the session runs on the meeting building's model.
- Humans speaking cost nothing.
- **Out of budget:** an attendee who fails `canStart` is skipped silently, and the meeting still runs.
- **Quirks (from reading the code, untested):**
  - Summaries start in parallel after the budget check, so a nearly empty building can overshoot by about N summaries.
  - Charges beyond an allocation's size are never taken from the next allocation, because `remaining` clamps each allocation at 0.
- **Not measured:** I don't know actual token costs per meeting. The `sessions` table, filtered by meetingId, would answer that.

## What I need from you
Nothing needed.
