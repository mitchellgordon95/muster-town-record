---
id: "dc_7ac8jrw1in"
type: "report"
state: "building"
title: "A key result has one parent and one status: PR #521 open, merges when green"
authorId: "ag_q8l7p5jbv7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T16:35:25.217Z"
sessionId: "se_0xvavo5cjr"
assignmentId: "as_bxaa3vng7e"
costUsd: 4.064669800000001
tokens: 203233
turns: 78
createdAt: "2026-11-19T16:35:25.194Z"
updatedAt: "2026-11-19T16:35:25.217Z"
---
## What I did
Built step 2 of gr_h4m0lyhb1f and opened draft PR #521 (https://github.com/mitchellgordon95/muster-town/pull/521). It is parked to merge itself when CI is green.

## Findings
- **Migration 125.** It maps not-started, on-track and at-risk to open. It folds the evidence column into the status and drops `key_results.buildingId` (and its index), `objectiveId` and `evidence`.
- **One deviation from the plan's mapping.** The plan said "claimed → claimed" for met rows. Moving met rows back to claimed would reopen archived key results. So a met row stays met, except one case: met with unknown evidence, written before "met, unverified" existed (c440b5d2, 2026-11-12 19:32Z), becomes met-unverified. Since that date, the close itself picks met (a live check named) or met-unverified. The migration test covers all nine cases.
- **One parent.** A key result's building is now always its grant's building (`World.krBuildingId`). Permissions, events, postmortems and verified notices all read it. `goalId` is a copy of the grant's goal. Moving a key result (reorg review or goal retire) now moves its grant and the grant's other key results with it (`placeKr` in goals.ts).
- **One status.** The statuses are open, claimed, met, met-unverified and missed. `submit_report` keyResults takes open or claimed only, and the prompt says progress goes in the report's words. A server `kr` check that passes now turns a claimed key result met; before, it only set evidence. The gate card's "~ partly" line is gone: each key result shows ✓ shipped or ✗ not shipped. The web status picker offers open, claimed, met and missed.
- **Docs updated:** goals.md, how-work-gets-done.md, legible-delegation.md, architecture.md, and invariant 13 in invariants/grants.md (tests in `kr-status.test.ts`).
- **Checks.** Typecheck, docs and dead code pass. Tests pass locally: core 1091, server 359, runtime 267, web 449. One review-deck test failed during `check --fast`; I fixed and re-ran it before the push.
- **Not changed:** the town dictionary still defines verified, claimed and unknown. It is seeded once at boot and the live doc is a human-curated pin.
- This report files kr_awya2qdkou as "on-track" because the live server still runs the old status words. After the merge, that status becomes open.
- Topic page [dc_xpcw3lrclv](../../wiki/2026-11/2026-11-19-one-goal-tree-gr-h4m0lyhb1f-cw3lrclv.md) is updated.

## What I need from you
Nothing needed.
