---
id: "dc_nq9jobf76j"
type: "report"
state: "building"
title: "PR #316: CI failed on deadcode (2 unused re-exports); fixed and re-pushed, parked on CI"
authorId: "ag_ygalarssqh"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Right call not to merge on red. Continuation as_qp3yehlilx already waits on {pr:316}: merge on green (re-check 089 is still the highest migration), park on the merge sha, verify backup.copies/backup.transcripts on live /api/health, rewrite dc_jyioru2ua3, tell Pix. If the test step fails in CI, find the failing test name in the CI log (not the desk tail) and fix it."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T18:43:23.205Z"
sessionId: "se_u9fehe0nxk"
assignmentId: "as_zsq2dtbg5r"
costUsd: 0.6045525
tokens: 30228
turns: 18
createdAt: "2026-11-04T18:43:16.871Z"
updatedAt: "2026-11-04T18:43:23.205Z"
---
## What I did
PR #316's first CI run failed at the `deadcode` step, so I did not merge it. The step flagged three unused exports in packages/server/src/backup/index.ts: the re-exports `parseTranscriptKey` and `transcriptKey`, and the exported `BackupSources` interface. I removed the two re-exports and made the interface module-local, committed that as a39406c2 and pushed it to the PR. I'm parked on its CI.

## Findings
- On my desk, `npm run check` now passes docs, deadcode and typecheck, and backup.test.ts passes (27/27).
- The full test step on the desk ended "FAILED at tests" after 9 min 57 s. I don't know which test failed: I only kept the tail of the output.
- Earlier per-package runs were green (server 283/283, core 727/727), so this may be a timing failure on a slow desk, but I have not confirmed that. CI's test step decides: in the first CI run it never ran, because deadcode stopped the check first.
- 089 is still the highest migration on origin/main, so 090 in the PR does not collide.
- **Next session:**
  1. If CI is green: merge, park on the merge sha, check `backup.copies` and `backup.transcripts` on the live /api/health, rewrite [dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md), and tell Pix.
  2. If a test fails: fix it.

## What I need from you
Nothing needed.
