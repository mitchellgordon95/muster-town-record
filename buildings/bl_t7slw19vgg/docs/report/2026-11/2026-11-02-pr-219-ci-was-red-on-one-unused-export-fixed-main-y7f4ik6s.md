---
id: "dc_9dy7f4ik6s"
type: "report"
state: "building"
title: "PR #219 CI was red on one unused export: fixed, main merged in, parked on CI again"
authorId: "ag_08w492gc69"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation as_r5u0kxfipp already waits on PR #219's CI and will merge, redeploy and report the live commit. Nothing more to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-02T03:44:31.141Z"
sessionId: "se_ok6udmrrka"
assignmentId: "as_6o3plknsp8"
costUsd: 0.4011161
tokens: 20056
turns: 13
createdAt: "2026-11-02T03:44:24.828Z"
updatedAt: "2026-11-02T03:44:31.141Z"
---
## What I did
PR #219's CI failed. The cause was `check:deadcode`: `GOAL_SIGN_H` in `packages/web/src/map/overlay.ts` was exported but nothing outside the file uses it. I unexported it and merged main into the branch. The merge had one conflict in the `renderer.ts` import line, which I resolved by keeping both `BANK_SIGN_H` and `placeGoalSigns`. I pushed head f958320 and marked the PR ready for review. It is not merged and no redeploy is queued yet.

## Findings
- **Locally:** typecheck and the docs and deadcode checks pass.
  - On the first full `npm run check`, 1 of 260 tests failed: a server timing assertion, `maxGap < 100`. This PR changes only web files, so it can't be the cause. It passed on the re-run, which looks like a flaky test under desk load.
- **PR:** https://github.com/mitchellgordon95/muster-town/pull/219
- **When CI is green:** merge #219, queue a redeploy, and report the merge commit as the one that should be live.
- **If CI is red again:** fix whatever it names first.

## What I need from you
Nothing needed.
