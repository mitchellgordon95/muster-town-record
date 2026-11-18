---
id: "dc_c231zeft5p"
type: "report"
state: "building"
title: "Exploration: proposed a work-versus-coordination split on the Bank (gr_3ougmyubdm)"
authorId: "ag_j3vx8tcn1d"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Findings verified against the code (finance-lane-kind.ts:81 manager row, finance-manager-wakes.ts:68 decidedBy-only count). Proposal gr_3ougmyubdm rendered as a money ask; Mitchell decides. Nothing queued."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-18T00:03:14.503Z"
sessionId: "se_7n47h5na7m"
assignmentId: "as_3gtsnqls9v"
costUsd: 1.0349744
tokens: 51749
turns: 24
createdAt: "2026-11-18T00:02:08.463Z"
updatedAt: "2026-11-18T00:03:14.503Z"
---
## What I did
Read the live finance endpoints (cbfa71e; check:finance all ✓) and the code behind the lane × kind table and manager wakes. Checked that the adjusted-token mix line and gr_lwgus14rd2's three key results are already live. Filed findings [dc_z24fd08cdp](../../note/2026-11/2026-11-18-findings-half-of-last-week-s-spend-was-managers-de-4fd08cdp.md) and proposal gr_3ougmyubdm: 350,000 tokens (M + M + S), under gl_vjek98yym0.

## Findings
- The 7-day `byLaneKind` from /api/finance/spend has 27,358,237 adj. tokens over 831 sessions. **Manager sessions: 13,244,281 (48%)**. Directed: 7.3M (27%). Grant: 4.7M (17%). Retainer: 0.93M. Exploration: 0.93M. The Bank has no sentence saying this. It shows only as one row in a toggled table on the Spending tab.
- `managerWakes` shows town-hall (the Secretary) with 338 wakes and 2,979,508 tokens, but **decided 0** ("no decisions"). The reason: finance-manager-wakes.ts counts only docs with `decidedBy`. It never counts ask ranks, folds, defers, overtakes or renders.
- The `daily` rows in /api/finance carry only building, so the chart cannot show whether coordination is growing. Bank debits have no session or lane, so the split has to come from session rows.
- The proposal adds a 7 d and 30 d work-versus-coordination sentence with a ✓ line under the Balance chart. It also splits the chart's bars into two tones (byLane per daily row, with a check) and counts the Secretary's ask actions as decisions. The history-based estimate is 329k–368k.

## What I need from you
Fund, counter or reject gr_3ougmyubdm.
