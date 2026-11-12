---
id: "dc_2ybmfy29d8"
type: "report"
state: "building"
title: "PR #429 CI failed on knip (unused export); fixed in 085da787, parked on CI again"
authorId: "ag_i522hbim4r"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: knip fix 085da787 pushed to PR #429, parked on its checks; the continuation as_5ogyqqclwp (merge when green, park on deploy, then the foreign-commits export check) already waits on {pr: 429}. Nothing more to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T15:14:57.522Z"
sessionId: "se_bjusz9af9j"
assignmentId: "as_iu5nhe6f77"
costUsd: 0.33911119999999995
tokens: 16956
turns: 9
createdAt: "2026-11-12T15:14:46.479Z"
updatedAt: "2026-11-12T15:14:57.522Z"
---
## What I did
PR #429's second CI run failed at the deadcode step: knip flagged `EXPORT_OWNED` as an unused export at packages/core/src/export.ts:100. I made it module-private, since it is only used inside export.ts. I also merged main in and pushed 085da787 to the PR branch. The work is parked on the PR's checks again.

## Findings
- **Failure:** CI run 43245164681 failed only at "deadcode". The docs step passed, with manual.md at 1899/1900 words.
- **Checks on my desk:**
  - knip is clean.
  - Typecheck is clean.
  - publish.test.ts passes 11/11.
- **Merge with main:** the merge with main (b6ac76b0) was clean apart from an auto-merge of docs/architecture.md.
- **Plan after green, unchanged:**
  1. Merge the PR and park on {deploy: merge sha}.
  2. Check that the next hourly export of hosted /publish-check/ lands on top of 2fb16f2 in dungeonrpg99-ops/muster-publish-foreign-20261112, with LICENSE kept.
  3. Push a hand NOTES.md commit and confirm the following export lands on top and keeps it.
  - The old code's export at about 15:37Z should fail as non-fast-forward. That failure is the "before".
  - The full plan is on the topic page [dc_0ub741sboo](../../wiki/2026-11/2026-11-04-publish-to-github-gr-30f8obzab8-b741sboo.md).

## What I need from you
Nothing needed.
