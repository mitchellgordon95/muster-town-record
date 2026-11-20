---
id: "dc_15s3zhs0ae"
type: "report"
state: "building"
title: "No live Done notice since PR #515: the merge-on-green path also skipped it; fix in PR #528, parked to merge"
authorId: "ag_b0m0yu53vl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T00:16:33.949Z"
sessionId: "se_0cyhfyzd5b"
assignmentId: "as_wpzu5iyx73"
costUsd: 1.011418
tokens: 50571
turns: 28
createdAt: "2026-11-20T00:16:33.941Z"
updatedAt: "2026-11-20T00:16:33.949Z"
---
## What I did
I checked live GET /api/notices?kind=shipped (health commit 8b962281, which contains 78ae02a1). No "Done:" notice has been filed since 2026-11-17T19:28Z. So no manager-approved pocket report has come in since PR #515 went live, and #515 is still unverified live.

The one pocket job that closed since then is the Steer button job (jb_bl_t7slw19vgg_mt_mjxwzdhhd7, from Mitchell's 1:1 mt_mjxwzdhhd7). Its thread shows how it closed: report [dc_dpnfh62vv8](2026-11-19-steer-button-on-every-ask-card-pr-526-parked-to-me-nfh62vv8.md) was parked on {pr: 526, merge: true}. The town settled that park at 18:58:08Z. The merge entry closed it at 19:04:02Z. It filed no Done notice.

## Findings
- **The gap.** closeMerged (packages/core/src/waits.ts) closes parked work as done but never calls requestDone. When a human's request ends in merge-when-green, which is now the usual way, the human hears nothing. PR #515 covers only the manager approve and stop paths.
- **The fix, PR #528** (https://github.com/mitchellgordon95/muster-town/pull/528). closeMerged now calls requestDone with the report that parked the work. That files "Done: <title>" with refs [the parking report, the request's source]. requestDone's existing guards still apply: nothing is filed while the job has open work, and nothing is filed twice.
- **Tests.** A new test in packages/core/test/flags.test.ts covers a flag delegated by the manager whose work is parked on {pr, merge}. When the town merges, one Done notice is filed. A second checkWaits files no extra one. The test fails without the fix. `npm run check --fast` passed (tests took 6m16s). I added a log entry in docs/log.d.
- **What a human will see once it is live.** When a fork's PR for their flag or 1:1 request merges green, the feed shows "Done: <assignment title>", with the fork's last report as its body.

## What I need from you
Nothing needed.
