---
id: "dc_kg708cu29y"
type: "report"
state: "building"
title: "503 follow-up C: PR #230 merged (97911e8), redeploy queued, image-deploy outbox filed; parked on the deploy"
authorId: "ag_qwaad0ggl8"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #230 merged at 97911e8, plain redeploy queued (brings #225 too); continuation as_an0yn18eop waits {deploy: 97911e8} to check the \"build server\" event and #225 health keys. The image deploy has its channel (outbox dc_lyjnyeev9f). The town-wide CI promote change (docs-only skip + 15-min debounce) goes in the next rollup's \"Your call\"."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T00:15:51.980Z"
sessionId: "se_3auw9xg1d6"
assignmentId: "as_8ta9rmx7bu"
costUsd: 0.6600184
tokens: 33001
turns: 20
createdAt: "2026-11-01T00:15:37.964Z"
updatedAt: "2026-11-01T00:15:51.980Z"
---
## What I did
- PR #230's CI passed on head 0de0994 (audit and check green; promote skipped as usual on a PR).
- Main had moved to e59619c (#225), so I test-merged it locally first. The merge was clean and added no migrations. Typecheck passed. The bundle built (6 files, 316 ms), booted on a fresh data dir, and `/api/health` returned ok with `figuresAt` and `load.tick`.
- Merged PR #230 (https://github.com/mitchellgordon95/muster-town/pull/230) at **97911e8**.
- Queued a plain `redeploy`. Live was still c3a49e3 at 00:14:53Z by my desk clock, so this redeploy also brings in #225 (e59619c).
- Filed one outbox request, [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), asking Mitchell to run `deploy/fly/build.sh` once (the town image deploy).
- Updated topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md).

## Findings
- **97911e8 should be live after this redeploy.** I haven't verified it yet. This session is parked until 97911e8 is live; then it checks that /api/events shows the redeploy's "build server … ok" step and that the #225 health keys are present.
- **No double restart expected.** CI's new promote job runs on the merge push. If the live commit already equals 97911e8 when it runs, nothing has changed since then, so it skips the redeploy. If the town redeploy is still draining when CI checks, CI waits until the server has been up 15 min and then restarts it once more. That costs one extra restart at most.
- **The faster boot isn't live yet.** Until the town image deploy runs, the image's entrypoint still starts the server with tsx, so the 0.87 s boot (vs 2.3–3.1 s with tsx) isn't in effect. The same image deploy also applies #225's 10 s health-check timeout.

## What I need from you
Run `deploy/fly/build.sh` once (outbox [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md)). Also note that PR #230 changes the town-wide CI promote job (no redeploy for docs-only changes, and at most one CI restart per 15 min); veto it in the rollup if you don't want that.
