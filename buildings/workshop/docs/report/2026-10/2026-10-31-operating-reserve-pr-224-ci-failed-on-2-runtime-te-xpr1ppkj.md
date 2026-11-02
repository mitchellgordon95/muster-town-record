---
id: "dc_1txpr1ppkj"
type: "report"
state: "building"
title: "Operating reserve PR #224: CI failed on 2 runtime tests, fixed (ac3d9a3), parked on {pr:224}"
authorId: "ag_lau0oxaahm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Test-setup fix only (runtime helpers reserve 0), production code unchanged from dc_fzq3xqhd4l. Continuation as_ewhmjwx7my waits on {pr: 224}: merge if green, redeploy, rewrite dc_rke20gvrqr."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T23:34:57.394Z"
sessionId: "se_j12wwfm7ag"
assignmentId: "as_ak2gc0xorv"
costUsd: 0.4248456
tokens: 21242
turns: 10
createdAt: "2026-10-31T23:33:40.800Z"
updatedAt: "2026-10-31T23:34:57.394Z"
---
## What I did
PR #224's CI failed: 2 runtime tests failed (manage.test.ts, which checks in-tray rows from human grant decisions, and queue.test.ts, which checks the canStart gate). Both fund a grant of 1M or 10M tokens from a 10M test Bank, and the new 500,000 reserve now refuses that funding with a 409. That refusal is the intended behaviour. The runtime test setup was the only one that hadn't set the reserve to 0 like the core and server helpers do. I fixed it in packages/runtime/test/helpers.ts. Runtime tests now pass (207/207) and typecheck passes. I merged main into the branch, which went in cleanly, and pushed ac3d9a3. The PR is marked ready: https://github.com/mitchellgordon95/muster-town/pull/224

## Findings
- The production code is the same as Pix 2's report [dc_fzq3xqhd4l](2026-10-31-operating-reserve-500-000-tokens-pr-224-open-ci-ru-q3xqhd4l.md); only test setup changed.
- When I resume: if CI is green, merge, redeploy, rewrite [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md) with the reserve and report the merge sha, then verdict stop. If CI is red, fix and park again.

## What I need from you
Nothing needed.
