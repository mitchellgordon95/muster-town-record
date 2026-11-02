---
id: "dc_50fai9onl1"
type: "report"
state: "building"
title: "Grant decisions now wake the manager (e8084c4 on main): fund → \"assign its first step\" grant-lane assignment with the plan, counter → \"Answer the counter\", reject → \"read the note\"; parked until it is live"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_5mxgn9gj16"],"urls":["https://github.com/mitchellgordon95/agent-town/commit/e8084c4f31c58dcb18e9e83c8f0903b63fdd9be5"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The live check is already queued as as_f6bfifiogd (the parked continuation resumed when e8084c4 deployed); no second assignment. Fold the live result into the next rollup."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T19:08:00.649Z"
sessionId: "se_1hghs2v2gf"
assignmentId: "as_t8ag8kacyd"
costUsd: 3.9110789499999994
tokens: 83295
turns: 41
createdAt: "2026-10-26T19:07:33.211Z"
updatedAt: "2026-10-26T19:08:00.649Z"
---
## What I did
- Added `Grants.decisionAssignment` in packages/core/src/grants.ts, called from `decide` for fund, counter and reject, next to the existing checkpoint hook. It creates one front-of-queue assignment for the building's manager agent (none when the building has no manager agent: a human works the in-tray).
  - **fund** → lane grant on the grant (key result implied), title `Grant <id> funded: assign its first step or take it yourself`; the description carries the funder's note, tokens, key result, approach, testing plan, stop condition and findings doc ids, and the three steps (cut the plan, `assign` the first step in lane grant, say who got what).
  - **counter** → directed, `Answer the counter on <objective>`, with the note and the new ask; points at `propose_grant` (re-proposes under the same id).
  - **reject** → directed, `Grant <id> rejected: read the note`; says the key result is open for exploration again.
  - Continue and adjust at a checkpoint create nothing (held grant work resumes on the next tick); cut still only sends the inbox line.
- Manager prompt (prompts.ts) says what the three wakes are; docs/goal-directed-budgets.md, docs/wakes.md (table rows + build-order step 3) and docs/log.md updated.
- Tests: three new cases in packages/core/test/lanes.test.ts (funded assignment with the plan and `canStart`; countered then rejected on the same proposal; no manager agent → nothing queued). The existing checkpoint test now counts only "Write the checkpoint" rows, since fund queues one assignment too.
- Verified: `npm run typecheck` green; core 273/273 and server 74/74 tests pass. Pushed straight to main as e8084c4 (Prod standing rule; no separate PR).

## Findings
- Muster Town's `redeploy` tool refuses me ("town.redeploy" permission), as in earlier sessions, so CI ships main. Live `GET /api/health` reports commit 76c6ad1 (one behind). Parked on `{deploy: e8084c4}`; next session checks the live commit and that the manager prompt carries the new line.
- Behaviour can only be seen end to end when Mitchell decides a proposal: the next fund/counter/reject on any building with a manager agent should put the assignment at the front of that manager's queue (`GET /api/agents/<manager>` assignments, or the building's board).
- A countered-then-re-proposed-then-rejected proposal wakes the manager once per decision (two assignments), which is intended: each carries a different note.

## What I need from you
Nothing needed.
