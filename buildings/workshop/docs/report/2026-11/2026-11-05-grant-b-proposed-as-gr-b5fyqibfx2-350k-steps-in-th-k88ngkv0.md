---
id: "dc_06k88ngkv0"
type: "report"
state: "building"
title: "Grant B proposed as gr_b5fyqibfx2 (350k): steps in the proposal, funding queues step 1, no kickoff session"
authorId: "ag_l6074j0t7y"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_y949h9jto6","dc_lq9eo4lz5a","dc_p73nckwcta"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grant B proposed as gr_b5fyqibfx2 (350k, 5 KRs due 11-08/11-09; plan dc_lq9eo4lz5a); it reaches Mitchell in the Town Hall in-tray on its own. Automatic next step on a step's report (pivot leaves it to the manager) is the right pick: no manager session per step. Nothing further."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T21:51:33.822Z"
sessionId: "se_ighxd88wio"
assignmentId: "as_3hdrsvyq02"
costUsd: 0.8142071999999999
tokens: 40710
turns: 20
createdAt: "2026-11-05T21:51:27.746Z"
updatedAt: "2026-11-05T21:51:33.822Z"
---
## What I did
Read the funding path on main fcdb0254: `Grants.decide` → `decisionAssignment` (packages/core/src/grants.ts ~809-835), `propose_grant` (core/src/verbs/grants.ts), `submit_report` (verbs/docs.ts ~314), GrantPanel.tsx and review-deck.ts. Wrote the plan as topic page [dc_lq9eo4lz5a](../../wiki/2026-11/2026-11-05-grant-b-steps-in-the-proposal-no-kickoff-session-9eo4lz5a.md) and filed the proposal. Nothing built, as asked.

## Findings
- **Proposal gr_b5fyqibfx2**: 350,000 tokens, goal gl_join, 5 key results due 11-08/11-09. They cover funding queuing step 1 with the kickoff assignment deleted (kr_mb8p4yqltw), the back-fill migration (kr_wvbva6xmw6), steps in propose_grant plus the card and deck (kr_snardl39qh), auto next step (kr_pag1dskg1o), and tests (kr_0nrodujj9e). Estimate line: "3 similar grants spent 189,110–950,081 (median spent/funded 0.90 across 46 closed grants; this building 0.98 across 7)".
- **The kickoff today** is the funded branch of `decisionAssignment`: a front-of-queue manager assignment, "Grant X funded: assign its first step or take it yourself", charged to the grant. B deletes that branch with no fallback. Funding creates step 1 directly on the building queue (lane grant, the step's model and pages). The counter and reject wakes stay.
- **Next step: automatic.** When a step's fork submits its report (not parked, verdict not pivot), the town queues the next step. A pivot queues nothing and leaves it to the manager's review. A manager stop or redirect cancels a next step that hasn't started yet. I chose this over "manager review continue" because it needs no manager session per step.
- **Migration 096** (renumber if main moves): adds `grants.steps` (JSON) and `assignments.grantStep`. It back-fills every draft, proposed or countered grant with one step, "Step 1: <objective>", as in the approach. Funded grants are untouched.
- Out of scope: grant C (checkpoint without a manager session). Closing after the last step still takes close_grant. Once B lands, grant A's kr_hlb6efq64i has no kickoff sessions left to measure.

## What I need from you
Fund, counter or reject gr_b5fyqibfx2 in the Town Hall in-tray.
