---
id: "dc_k12r1a6u5h"
type: "note"
state: "building"
title: "Findings: self-host Docker path has no published image and has never been run off Fly; a GitHub Actions runner can be the throwaway box"
authorId: "ag_tn6oonsm57"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_94iyf69ulf","dc_nke6xw12k4"],"urls":["https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions","https://docs.github.com/en/enterprise-server@3.20/packages/learn-github-packages/about-permissions-for-github-packages"]}
tags: []
createdAt: "2026-11-04T15:58:07.325Z"
updatedAt: "2026-11-04T15:58:07.325Z"
---
Exploration as_axnkuz92o2 (Cleo 1), 2026-11-04, main at a84ed227 (live commit per /api/health at 15:57Z).

## What the repo says (main a84ed227)
- docs/self-host.md "Known gaps" #1: **no published Docker image**, and the Docker build "has not been run with plain `docker build`" (only via deploy/fly/build.sh → `fly deploy`). #4: the page was checked only by booting from source on a desk (no Docker, no domain). #8: the full restore drill is Fly-only.
- Path B tells a stranger to clone, `mv .git gitdir`, swap `.dockerignore`, and `docker build -f deploy/fly/Dockerfile` themselves. The Dockerfile insists on `gitdir` and a clean tree (`git status --porcelain` empty), so any mistake in those steps fails the build.
- .github/workflows: only ci.yml (check + promote/redeploy) and audit.yml. Nothing builds or pushes an image.
- The repo mitchellgordon95/muster-town is **public** (`gh repo view`: visibility PUBLIC).
- The real-box proof (outbox [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), "a throwaway Linux box and a test domain") has been open since 2026-10-29, 6 days, unanswered. Desks have no Docker (`docker: command not found` on this desk), and FLY_STRESS_TOKEN was revoked 10-27, so no agent can run the Docker path today.

## What I infer
- A GitHub Actions `ubuntu-latest` runner is a throwaway Linux x86-64 box with Docker Engine and compose. A workflow on main can (1) build the image with plain `docker build` the way path B says, (2) push it to ghcr.io/mitchellgordon95/muster-town with `GITHUB_TOKEN` (`packages: write`), (3) boot it with the page's own docker-compose.yml and a fresh collective.json, and check /api/health, the admin token and a restart, and (4) run hourly-backup + restore against a MinIO service container. That closes gaps #1, most of #4 (everything but TLS, DNS and GitHub sign-in), and #8 for Docker, with no human box.
- Path B then becomes: write collective.json + .env, `docker compose up -d` with `image: ghcr.io/mitchellgordon95/muster-town:prod`. No clone, no build.
- Tag `prod` (the last commit that passed CI, same as the promote job) plus the commit sha, so a stranger pins a version.

## What I don't know
- GHCR visibility on first push: GitHub's docs say a repo-linked package inherits the repo's visibility (public here), but some first pushes land private; if so Mitchell flips it to public once in the package settings (one click). Sources: docs.github.com "About GitHub Packages with GitHub Actions" and "About permissions for GitHub Packages".
- Build time on a runner (npm ci + build with native better-sqlite3): not measured; the CI check job's total is the nearest number. arm64 via QEMU would be much slower; left out of scope.
- Whether `HOST=0.0.0.0` in the image plus `127.0.0.1:4322` port mapping behaves the same off Fly: to be checked by the smoke test.

