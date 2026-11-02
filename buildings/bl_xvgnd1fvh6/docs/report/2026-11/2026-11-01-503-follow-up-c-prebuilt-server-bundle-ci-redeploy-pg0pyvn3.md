---
id: "dc_mzpg0pyvn3"
type: "report"
state: "building"
title: "503 follow-up C: prebuilt server bundle + CI redeploy coalescing, PR #230 open; parked on CI"
authorId: "ag_hlif0j4hz3"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Continuation as_8ta9rmx7bu (waits {pr: 230}) merges when green and does a plain redeploy. The CI promote-job change (docs-only skip + 15-min debounce) goes in the next rollup as a \"Your call\" so Mitchell can veto it; the town image deploy for the new entrypoint goes through one outbox request as planned."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T00:06:25.890Z"
sessionId: "se_regcp8uaui"
assignmentId: "as_jqg05a2ztx"
costUsd: 2.882444900000001
tokens: 144122
turns: 56
createdAt: "2026-11-01T00:06:13.194Z"
updatedAt: "2026-11-01T00:06:25.890Z"
---
## What I did
- Measured boot cost on the live town and on my desk.
- Opened PR #230 (https://github.com/mitchellgordon95/muster-town/pull/230):
  - the server is prebuilt to JS with esbuild and started with plain node, with a fallback to tsx;
  - the redeploy gets a "build server" step;
  - CI skips docs-only redeploys and allows at most one CI restart per 15 min.
- Local `npm run check` is green (8m05s, all tests passing). Parked until PR #230's CI finishes.

## Findings
- **Live boot today**, from /api/events, 6 redeploys between 22:50Z and 23:49Z:
  - "restarting" → "finished" took 3.1–3.5 s.
  - "build web" took 7.3–10.8 s per redeploy, so it costs more CPU per deploy than the boot. This PR doesn't address that.
  - I couldn't break the boot into tsx, migrations and waker replay: `fly logs` isn't reachable from a desk.
- **Boot CPU to the first /api/health** (desk, 2 vCPU, seeded town, 3 runs each):
  - tsx: 3.1 s cold cache, 2.3 s warm.
  - prebuilt bundle: **0.87 s**.
  - Building the bundle takes about 0.3 s.
- **How it works:**
  - `packages/server/build.mjs` writes `packages/server/dist` (gitignored) plus `BUILD_HEAD`, the commit it was built from.
  - `deploy/fly/start-server.sh` lives in the checkout, so later changes ship with a normal redeploy. It runs the bundle only when `BUILD_HEAD` matches HEAD; otherwise it rebuilds, and if that fails it runs tsx as before.
  - Small path fixes so the runtime, the backup worker and the migrations are found both from the sources and from the bundle.
  - Dev, tests and `scripts/serve.sh` keep using tsx.
- **CI (`.github/workflows/ci.yml`, promote job only):**
  - No redeploy when everything since the live commit is under `docs/` (except `docs/manual.md`, which the server serves), `.github/` or a top-level `*.md`.
  - If the server started less than 15 min ago, the job waits out the rest. A newer push cancels the waiting run and redeploys its own commit.
  - I dry-ran this logic against code changes, docs-only changes, a manual.md change, an unknown live commit and an unreachable health check.
  - The repo is public, so the waiting costs no Actions minutes.
- **Catch:** the Fly entrypoint is baked into the town image. The live town keeps starting with tsx until the next **town image** deploy (`deploy/fly/build.sh`). A `redeploy` with image: true only rebuilds the desk image. The same image deploy also applies PR #225's 10 s health-check timeout.
- **Plan for the next session** (also on topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md)):
  1. CI green → merge.
  2. Plain redeploy; check that /api/events shows "Redeploy: build server … ok".
  3. File one outbox request to Mitchell for the town image deploy.
  4. After that deploy, read the restarting → finished gap as the "after" number.

## What I need from you
This PR changes the town-wide CI workflow (ci.yml promote job: docs-only skip plus a 15-min debounce), so say in the rollup if you want to veto it. The manual `redeploy` tool is unchanged.
