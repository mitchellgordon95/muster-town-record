---
id: "dc_129fjnr9mh"
type: "report"
state: "building"
title: "PR #250: CI failed on a3f17c1 because main is red at deadcode (Pix's new unused exports); fixed in 07895b6 on the merged branch, parked on CI"
authorId: "ag_rlo66fvv62"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked step-1 report: PR #250 CI failed on a3f17c1 only because main is red at deadcode (Pix's unused exports); merged 01ccc8e, unexported 4 symbols, local check green, pushed 07895b6. Continuation as_zwrb8nkzw0 waits on {pr: 250} and carries mark-ready, merge, {deploy} park and live verification. Nothing else queued."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-02T03:22:22.372Z"
sessionId: "se_3ydqjuufxy"
assignmentId: "as_2eavydncvl"
costUsd: 0.4496608
tokens: 22483
turns: 12
createdAt: "2026-11-02T03:22:14.260Z"
updatedAt: "2026-11-02T03:22:22.372Z"
---
## What I did
- PR #250's CI on a3f17c1 **failed at check:deadcode** (run 41382045804). The failure isn't from our code: main itself is red at deadcode since 88bcbf3 and f72fe63, and 01ccc8e adds one more unused export.
- Merged origin/main (01ccc8e) into the PR branch. There were no conflicts.
- Dropped `export` from 4 unused symbols, with no behaviour change:
  - `HOSTED_CAP_LINE` (web BankFunding.tsx)
  - `HelpThing` and `HelpCard` (web helpCard.ts)
  - `FounderRoad` (server hub.ts)
- Ran `npm run check` locally in the foreground: green in 4m55s. Results:
  - docs ok, manual at 1898/1900 words
  - deadcode clean, typecheck ok
  - tests: runtime 217, server 260, cli 25, desk 40, web 237
- Pushed merge 5defbb3 and fix 07895b6 to the PR branch.
- Told Pix (ms_6xz1g5c16z) not to push a separate fix that would conflict.

## Findings
- The unexport touches Workshop and Bank-UI files. It only removes the `export` keyword so main's own gate passes; there is no logic change, and no Bank or token-accounting logic is touched.
- Until #250 merges, main stays red at deadcode for every building.
- **Plan on resume:**
  1. If CI is green and main hasn't moved: `gh pr ready 250`, then `gh pr merge 250 --merge`. Don't call redeploy.
  2. If main has moved: merge it again and re-run check:docs and check:deadcode before merging.
  3. Park on {deploy: merge sha}, then verify live:
     - /api/health shows the merge commit
     - /api/town has no Ada and no kind service
     - /api/roles has no role:moderator and no role:&lt;bid&gt;:reviewer
     - every building still has its manager

## What I need from you
Nothing needed.
