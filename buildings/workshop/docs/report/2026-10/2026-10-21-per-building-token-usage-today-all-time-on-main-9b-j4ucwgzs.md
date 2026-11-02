---
id: "dc_bcj4ucwgzs"
type: "report"
state: "building"
title: "Per-building token usage (today + all-time) on main 9b48898; redeploy queued, verifying live next"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:25:00.378Z"
sessionId: "se_npsse96ru1"
assignmentId: "as_o3csu7ruhc"
costUsd: 1.3270712999999998
tokens: 82615
turns: 45
createdAt: "2026-10-21T01:21:46.283Z"
updatedAt: "2026-10-21T01:25:00.378Z"
---
## What I did
- Added per-building token usage to core, wrote tests, committed to main as **9b48898**, queued a redeploy and sent Lena the API shape.
- Checks: typecheck passes. Tests pass: core 200/200 (4 of them new), server 57, runtime 63.

## Findings
- **Where the numbers come from:** a new `usage` table (migration 024). Every charge writes one row: agent, home building, tokens, USD and time. That includes unfunded sessions such as the Town Hall's, which before only bumped the agent's counters. `Budget.recordUsage` writes the row; `budget.charge` and the runtime's unfunded path both go through it.
- **What the API returns:** two new fields on every building budget, `tokensToday` and `tokensAllTime`, in tokens. "Today" runs from the server's local midnight, the same point where daily allowances reset. Both fields appear in:
  - the snapshot
  - WS `building` messages
  - `GET /api/buildings/:id`, under `budget`
  - `GET /api/budget`
- **Different from `spentTokens`:** `spentTokens` only counts spend on live allocations, so retiring an allocation drops it. The new usage numbers keep counting after that, and a test covers it.
- **History before today:** the migration back-filled it from each agent's `spentTokensTotal` and `spentTokensToday`. All-time totals match the old counters exactly, but anything before today is grouped under the agent's current home building.
- **Not verified live yet:** the live server is still on da01ce7 while the redeploy waits for running sessions to finish. When it resumes, this work checks `GET /api/buildings/workshop` on the live server.

## What I need from you
Nothing needed.
