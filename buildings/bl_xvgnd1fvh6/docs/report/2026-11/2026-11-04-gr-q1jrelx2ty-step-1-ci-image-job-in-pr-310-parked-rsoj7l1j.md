---
id: "dc_jqrsoj7l1j"
type: "report"
state: "building"
title: "gr_q1jrelx2ty step 1: CI image job in PR #310, parked on its CI"
authorId: "ag_d7yvkf4e1e"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: step 1's continuation already sits on the queue as as_7v5rv0rfir (waits on PR #310's CI: merge on green, park 20 min, verify the image job + anonymous ghcr tags/list). No second assignment needed. Steps 2–4 follow on that report."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T17:58:50.365Z"
sessionId: "se_wewkwl2ea6"
assignmentId: "as_lq4hamzk1m"
costUsd: 0.4379541
tokens: 21898
turns: 9
createdAt: "2026-11-04T17:58:26.174Z"
updatedAt: "2026-11-04T17:58:50.365Z"
---
## What I did
Added an `image` job to .github/workflows/ci.yml (needs check, push-to-main only, beside promote, packages: write, 30 min, amd64). It clones the public repo fresh at $GITHUB_SHA on branch main, renames .git to gitdir, uses deploy/fly/dockerignore, runs a plain `docker build -f deploy/fly/Dockerfile`, then pushes `:<sha>` and `:prod` to ghcr.io/mitchellgordon95/muster-town and writes the digest to the log and the job summary. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/310

## Findings
- The PR run only exercises `check`. The image job first runs on the merge to main.
- On resume: merge on green, then park {after: merge + 20 min}. Then check `gh run view` for the image job's build time and digest, and the anonymous ghcr tags/list for `prod` and the merge sha. A 401/403/404 means the package is private: ask Mitchell to flip it public.

## What I need from you
Nothing needed.
