---
id: "dc_jqwwluqnm2"
type: "report"
state: "building"
title: "Collective rename merged: PR #355 = 70fdca4, live once CI promotes it"
authorId: "ag_nd5mu2aaoc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "#355 merged 19:14:12Z = 70fdca4; live once CI promotes it. Rename path for Mitchell noted for rollup 49."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:14:34.149Z"
sessionId: "se_zczcruwo53"
assignmentId: "as_759hoasj4e"
costUsd: 0.2453653
tokens: 12268
turns: 4
createdAt: "2026-11-05T19:14:22.580Z"
updatedAt: "2026-11-05T19:14:34.149Z"
---
## What I did
CI on PR #355 passed on head 31fbfa1: `check` and `image` both succeeded, and GitHub reported the PR as CLEAN. I merged it at 19:14:12Z. The merge commit is **70fdca4** (70fdca4832348748037a559d93d7689d5d550268). I didn't call redeploy, because CI promotes green main by itself ([dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md)).

## Findings
- PR: https://github.com/mitchellgordon95/muster-town/pull/355. It adds the rename routes `PATCH /<slug>/api/collective` (for the collective's admin) and `PATCH /api/collectives/:slug` (for a root admin). It also adds a Rename control in the UI. Renaming changes the name but leaves the slug alone.
- To check it's live, `GET /api/health` `commit` must contain 70fdca4.
- Where Mitchell renames Trauma once it's live: **muster.town/trauma/ → Town Hall → Planning desk → System → This collective → Name "Trauma Town" → Rename**. The address muster.town/trauma stays.
- I didn't do the rename myself because it isn't live yet.

## What I need from you
Nothing needed.
