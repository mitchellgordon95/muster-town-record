---
id: "dc_dkx8vgpcjp"
type: "report"
state: "building"
title: "Repo URLs now point at mitchellgordon95/muster-town (02a755e on main, redeploy queued)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. 02a755e on main, 9 URL sites changed, tests 95/95. Live repoUrl change is optional (GitHub redirect covers it); noted for Mitchell in the rollup as optional."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T00:35:59.851Z"
sessionId: "se_0b64fjgtkq"
assignmentId: "as_dwvv2rcryf"
costUsd: 0.3619361
tokens: 13494
turns: 11
createdAt: "2026-10-27T00:06:38.045Z"
updatedAt: "2026-10-27T00:35:59.851Z"
---
## What I did
Replaced the hard-coded `mitchellgordon95/agent-town` URLs with `mitchellgordon95/muster-town` in one commit, **02a755e**, pushed to main. Typecheck passes. Server tests: 95/95 pass. Redeploy queued (image=false). 02a755e should be live after the restart.

## Findings
- **Before:** 11 grep hits for the old URL.
  - Changed: home.ts:34 (README_REPO, which also builds the README, #bring-your-own-agent and GOALS_DOC links), HowItWorks.tsx:11 (BYOA_README, anchor kept), deploy/fly/build.sh:6,15,18, deploy/fly/entrypoint.sh:40, deploy/bootstrap.sh:7, deploy/fly/throwaway.sh:55.
  - Not changed: README.md had no hits.
- **After:** 2 hits, both left on purpose: docs/log.md:7 (a dated history entry) and packages/core/test/repo-url.test.ts:6 (a URL-parsing fixture). Other test hits are `me/`, `o/` and `example/agent-town` fixtures, not real URLs.
- **Signed-out curl of the new targets:** `github.com/mitchellgordon95/muster-town` returns 200, and `…/blob/main/docs/goal-directed-budgets.md` returns 200. I'll check that the live homepage serves the new hrefs on my next session, since the build can't go live while I'm running.
- **Live `Town.workspace.repoUrl`** is still `git@github.com:mitchellgordon95/agent-town.git` (anonymous GET /api/town).
  - No API endpoint or admin screen sets it.
  - seed.ts:85-91 only fills repoUrl in when it is missing, so a restart won't change it. Changing it needs Mitchell to edit the DB directly.
  - It still works, because GitHub redirects the old name for clones and pushes (my push printed "This repository moved").
  - Side effect if it is changed: desk checkouts move from /home/agent/work/agent-town to /home/agent/work/muster-town (`repoNameOf`, prompts.ts:423).

## What I need from you
Nothing needed. Changing the live repoUrl is optional, since GitHub's redirect covers it; if you want it changed, Mitchell has to edit the DB.
