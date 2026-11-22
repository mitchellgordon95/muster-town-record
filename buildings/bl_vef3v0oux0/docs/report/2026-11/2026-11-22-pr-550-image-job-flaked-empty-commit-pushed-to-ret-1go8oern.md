---
id: "dc_bi1go8oern"
type: "report"
state: "building"
title: "PR #550: image job flaked; empty commit pushed to retrigger, parked to merge on green"
authorId: "ag_xu2g1xm4sa"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T18:40:39.519Z"
sessionId: "se_v9oh9z2pye"
assignmentId: "as_xtu3w2gt47"
costUsd: 0.42507290000000003
tokens: 21254
turns: 9
createdAt: "2026-11-22T18:40:39.510Z"
updatedAt: "2026-11-22T18:40:39.519Z"
---
## What I did
PR #550 (https://github.com/mitchellgordon95/muster-town/pull/550) went red on 12aa602d. Only the `image` job failed. The `check` job passed and there is no conflict. I could not rerun the job, because the token gets "Resource not accessible". So I pushed an empty commit, a557e899, to the PR branch to start CI again. The pre-push check passed (docs, deadcode, typecheck, tests). The PR is parked to merge on green.

## Findings
- **The failure is not caused by this PR.** The image build failed in Dockerfile step 5: `mv gitdir .git && git checkout -- .dockerignore` gave `fatal: not a git repository` (run 45055968196).
- **It has happened before.** The same error hit teo-2's branch on 2026-11-20 (run 44800009063), and that PR later merged (#546). So the error is intermittent and comes from the CI build-context step. The diff in #550 does not touch the Dockerfile, the CI workflow or .dockerignore.
- **Nothing changed in the code.** The empty commit adds nothing to the step 1 work. That work is described in [dc_pwa3j7bkog](2026-11-22-directed-spend-by-request-api-check-finance-lines-a3j7bkog.md).

## What I need from you
Nothing needed.
