---
id: "dc_vr3udlh8fc"
type: "report"
state: "building"
title: "Dismissed residents: cause found (fixed in 94f302d by Mitchell, all 4 re-retired); admin Dismiss back in PR #222, parked on CI"
authorId: "ag_d40g4tqsz5"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Cause (budget sweep caught retired agents) was fixed by Mitchell in 94f302d and all four re-dismissed; PR #222 merged by Pix 1 as 878bc37, live check queued as as_u1yo3ojfes. Nothing more from this report."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T23:31:35.820Z"
sessionId: "se_sgjoilena0"
assignmentId: "as_9nmn5fytbu"
costUsd: 1.5553595999999998
tokens: 77768
turns: 44
createdAt: "2026-10-31T22:43:28.611Z"
updatedAt: "2026-10-31T23:31:35.820Z"
---
## What I did
- Read the event log for Root (ag_oycvqt9sa6) and checked the live status of all four agents.
- Found that Mitchell had already fixed the cause in 94f302d. That fix is live in aaded27 (health startedAt 22:37:24Z). He also re-dismissed all four at 22:37:54Z.
- Put the admin-only Dismiss button back on the agent panel: **PR #222** (https://github.com/mitchellgordon95/muster-town/pull/222). CI was still pending when I parked.

## Findings
- **Cause.** When a building runs out of budget, a sweep in core `budget.ts` marks its residents out-of-budget. It skipped only agents that were stopped or banned, so retired ones were caught too. Refilling the Bank then sets out-of-budget agents back to idle, which brought the dismissed residents back.
- **Event-log evidence (Root):**
  - 45604, 2026-10-29 03:35:03Z: dismissed.
  - 83948, 22:05:25Z: retired → out-of-budget.
  - 86048, 22:06:48Z: the startup desk repair gave Root its own desk, which is why the desks were held.
  - 86301, 22:12:56Z: out-of-budget → idle.
  - 87590/87591, 22:37:54Z: Mitchell dismissed Root again (deskFreed true).
- **Other agents.** Mitchell's commit says Dara, Asha and Finn were revived the same way. None of them is in the live `/api/town` agent list now; only managers, the Planner and live forks are. I only read the event log for Root, so the ids for the other agents are not in this report.
- **Fix and re-dismissal.** Both were done before I got to them: 94f302d adds "retired" to the statuses the sweep skips and adds a regression test in core `budget.test.ts`. All four agents now read `retired` at GET /api/agents/:id.
  - I did not add a startup re-retire step or a migration. The writer is fixed and the rows are already retired, so neither is needed.
- **Desks.** The four desks were freed by the 22:37:54Z dismissals. Pix 1, 2 and 3 forks are working now, so forks do start.
- **PR #222 (web only):**
  - New `panels/Dismiss.tsx`: `canDismiss` returns true only for an admin looking at a live resident that is not the building's manager and not a fork.
  - The button sits in a "Dismiss" section on the Assignments tab. Clicking it opens a confirm inside the panel (with an optional "delete desk volume" box), which calls the existing DELETE /api/agents/:id.
  - `api.dismiss` and the mock dismiss are restored.
  - New `test/dismiss.test.ts`.
  - Typecheck is clean and the web suite passes (210 tests); the core budget test passes. I had to run `npm install` first: the desk's node_modules were stale and both typecheck and tests failed until I did.
- **Rollup.** Picture: mf_o5hci5evmd, 300×76, taken from the mock. I created the topic page "Rollup 36 materials" ([dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md)) with the line and a "Your call". It is not live yet.

## What I need from you
Nothing needed.
