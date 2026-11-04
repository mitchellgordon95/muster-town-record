---
id: "dc_cqgy0imoti"
type: "report"
state: "building"
title: "Exploration: self-host Docker path has no image and was never run off Fly; proposed gr_q1jrelx2ty (220k) to publish one from CI and prove it on a GitHub runner"
authorId: "ag_tn6oonsm57"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_k12r1a6u5h","dc_nke6xw12k4","dc_94iyf69ulf"],"urls":["https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done; gr_q1jrelx2ty reaches Mitchell on its own in the Town Hall in-tray. Nothing to queue until it is decided."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T15:59:41.479Z"
sessionId: "se_ou13ts7ya5"
assignmentId: "as_axnkuz92o2"
costUsd: 0.8020600999999999
tokens: 39603
turns: 15
createdAt: "2026-11-04T15:58:36.714Z"
updatedAt: "2026-11-04T15:59:41.479Z"
---
## What I did
Read docs/self-host.md, deploy/fly/{Dockerfile,build.sh,entrypoint.sh} and .github/workflows on main (a84ed227, also the live commit). Checked that the repo is public and that desks have no Docker, and looked up how GHCR sets package visibility. Wrote findings [dc_k12r1a6u5h](../../note/2026-11/2026-11-04-findings-self-host-docker-path-has-no-published-im-2r1a6u5h.md) and topic page [dc_55z71al37g](../../wiki/2026-11/2026-11-04-self-host-image-gr-q1jrelx2ty-z71al37g.md), and proposed gr_q1jrelx2ty.

## Findings
- Known gaps in self-host.md: #1 says there is no published Docker image and the build has never been run with plain `docker build` (only through `fly deploy`). #4 says the page was never proven on a real box. #8 says the restore drill only works on Fly. The real-box request [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) has been open for 6 days with no answer, and no desk can run Docker.
- A GitHub Actions runner is a throwaway Linux box with Docker. A CI job can build the image the way path B describes and push it to ghcr.io/mitchellgordon95/muster-town as :prod and :<sha>. It can then boot it with the page's own compose file and check health across a restart, then back up to a MinIO container and restore into a second container. That closes gaps #1 and #8 and most of #4 (TLS, DNS and GitHub sign-in still need a real domain).
- Proposal gr_q1jrelx2ty asks for 220,000 tokens under ob_kdym3851tm. Free tokens are 489,983, and the town's estimate for similar grants is 77k–247k. It has 4 key results due 11-08 to 11-10. It only touches Prod's CI and deploy files and docs/self-host.md.
- Not known yet: the runner build time, and whether the first GHCR push comes out public. GitHub's docs say a repo-linked package inherits the repo's visibility, but this is not verified.

## What I need from you
Fund, counter or reject gr_q1jrelx2ty in the Town Hall in-tray.
