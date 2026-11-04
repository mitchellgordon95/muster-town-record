---
id: "dc_rrs07qgya4"
type: "report"
state: "building"
title: "PR #316: CI failed on a migration-number clash (main took 090); renumbered to 091, parked on CI"
authorId: "ag_pey56fq5jo"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: migration clash (main took 090) fixed by renumbering to 091 (074b3498). Continuation as_a818wyc7qe waits on {pr:316} and already covers merge-on-green + health check + tell Pix. Folds into the next rollup once the merge sha is live."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T18:49:31.902Z"
sessionId: "se_14ovni9vf6"
assignmentId: "as_qp3yehlilx"
costUsd: 0.368277
tokens: 18414
turns: 9
createdAt: "2026-11-04T18:49:19.260Z"
updatedAt: "2026-11-04T18:49:31.902Z"
---
## What I did
PR #316's second CI run failed at the test step. While the PR was open, main merged its own `090_join_funnel_visitors.sql`, so migrate() refused two migrations numbered 90 (the CI log shows the error in walk-home.test.ts, among others).

I merged origin/main into the PR branch, renamed our migration to `091_backup_detail.sql` and pushed that as 074b3498. I'm parked on the new CI run.

## Findings
- On my desk after the fix: typecheck passes, backup.test.ts passes 27/27, and walk-home.test.ts passes 6/6.
- No code refers to the migration file by name, so the rename needed no other edits.
- **Next session:**
  1. If CI is green: check that 091 is still free on main, merge, and park on the merge sha.
  2. Once that sha is live: check `backup.copies` and `backup.transcripts` on /api/health, rewrite [dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md), and tell Pix.
  3. If CI fails again: read the failing test name in the CI log.

## What I need from you
Nothing needed.
