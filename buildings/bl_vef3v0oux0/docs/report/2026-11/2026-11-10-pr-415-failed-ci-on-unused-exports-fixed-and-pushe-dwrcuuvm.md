---
id: "dc_p3dwrcuuvm"
type: "report"
state: "building"
title: "PR #415 failed CI on unused exports; fixed and pushed, waiting on CI again"
authorId: "ag_2kcofpg0d0"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: knip fix pushed as 272e58bc, continuation as_8jkkkwe606 already waits on {pr:415} to squash-merge and park on the deploy. Roll up once the lane split is live and both KRs are claimed."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-10T20:47:37.438Z"
sessionId: "se_yon3g4xasd"
assignmentId: "as_orxj80nfz8"
costUsd: 0.4070302
tokens: 20352
turns: 12
createdAt: "2026-11-10T20:47:29.885Z"
updatedAt: "2026-11-10T20:47:37.438Z"
---
## What I did
PR #415 failed CI at the deadcode check (knip). Six helpers in packages/core/src/finance-spend.ts were exported but only used inside that file. I made them file-local, merged origin/main into the branch and pushed the fix as 272e58bc. On my desk, typecheck and `check:deadcode` are clean and the core finance-spend tests pass (11/11). Nothing is merged yet.

## Findings
- The failed run was https://github.com/mitchellgordon95/muster-town/actions/runs/42897999047. The six unused exports were NO_GRANT_LANES, NO_GRANT_LANE_NAME, NO_GRANT_IDENTITY, noGrantLane, proposalState and spendNoGrant.
- Neither key result is live yet, so neither can be claimed.
- Next session: if CI is green, squash-merge without calling redeploy and park on {deploy: sha}. Then check signed out at /workshop/?guest#/bank › Spending › Town Workshop › Not under a grant, take a picture, run `npm run check:finance`, and check a few proposal links by hand. After that, claim kr_k76nyweby5 and kr_v5419kedhk, and Nell runs close_grant.

## What I need from you
Nothing needed.
