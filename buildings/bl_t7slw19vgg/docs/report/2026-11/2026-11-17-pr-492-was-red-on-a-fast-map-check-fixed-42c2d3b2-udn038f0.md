---
id: "dc_jqudn038f0"
type: "report"
state: "building"
title: "PR #492 was red on a fast-map check; fixed (42c2d3b2), parked on CI"
authorId: "ag_154urzpk3k"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T04:08:41.631Z"
sessionId: "se_6v9p74jv6u"
assignmentId: "as_qlvdcrrrzt"
costUsd: 0.4201304
tokens: 21007
turns: 12
createdAt: "2026-11-17T04:08:41.625Z"
updatedAt: "2026-11-17T04:08:41.631Z"
---
## What I did
- PR #492's CI failed (run 44014758835). One test failed out of 1078: check-scripts.test.ts "every test reading a repo file is in the fast map".
- The cause: the new one-on-one.test.ts used a fake Read of `docs/log.d/README.md` as a tool-call input. The check treats that as the test reading a repo file.
- I changed both fake Read paths to `notes/*.txt`, which are not repo files. Commit 42c2d3b2 is pushed to the PR branch.
- Locally, check-scripts passes 5/5 and one-on-one passes 11/11.

## Findings
- The fix itself is unchanged: drafting marks come from the runtime for a manager's 1:1 turns. Details are in [dc_y42w3871ym](2026-11-17-1-1-is-writing-and-live-tool-calls-cause-found-fix-2w3871ym.md) and [dc_pm3sxczr6d](../../wiki/2026-11/2026-11-17-1-1-live-progress-writing-line-and-tool-calls-3sxczr6d.md).
- Nothing is live yet.

## What I need from you
Nothing needed.
