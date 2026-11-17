---
id: "dc_4s6sr4xhbe"
type: "report"
state: "building"
title: "Server pulls its own deploys: PR #495 open, parked on CI"
authorId: "ag_srtxjt3v5h"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The continuation (as_5im5b2klh7) waits on PR #495's CI and merges it. When that merge lands, the report's \"an admin presses redeploy once\" becomes a click ask for Mitchell, which I file from the merge report."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-17T18:34:02.227Z"
sessionId: "se_z5rnjtqhw8"
assignmentId: "as_zc6ejtf2hk"
costUsd: 2.3782234000000004
tokens: 118911
turns: 35
createdAt: "2026-11-17T18:33:43.235Z"
updatedAt: "2026-11-17T18:34:02.227Z"
---
## What I did
Built the server-side puller and removed CI's redeploy step in one PR: https://github.com/mitchellgordon95/muster-town/pull/495 (draft, branch agent/cleo-1/server-pulls-its-own-deploys-runtime-wat). Parked on its CI.

## Findings
- `packages/runtime/src/prod-watch.ts` starts in startRuntime. It is on only with MUSTER_TOWN_DEPLOY_BRANCH, a git origin and a non-hosted collective.
- Every 60 s it fetches origin/prod. When prod is a fast-forward of world.host.commit with a deployable change, it calls the existing redeploy with requestedBy "prod branch" and image false.
- Guards:
  - It skips a tick while a redeploy runs or the repo lock exists.
  - Docs-only changes never restart it. The filter moved to schema `deployable`, and the `deploy` monitor key imports the same function, so the two agree.
  - Spacing is 10 min (PULL_SPACING_MS) after the server's start and after its own last request.
  - The same tip is retried only after 1 h.
  - When nothing is ahead, nothing is called.
- A fetch error writes one system event, then stays quiet until a fetch works (one more event).
- ci.yml promote only fast-forwards prod now. The redeploy step and every MUSTER_TOWN_DEPLOY_TOKEN reference are gone, and the timeout is cut from 25 to 5 min. Mitchell can delete that secret in GitHub.
- Docs updated: deploy/README.md ("CI and redeploy", "Live behind prod"), docs/architecture.md, the redeploy tool's text, and a docs/log.d entry.
- Not changed, as asked: POST /api/admin/redeploy, the `redeploy` tool, and {deploy} waits.
- Tests: runtime/test/prod-watch.test.ts has 6 tests: ahead → one redeploy; docs-only; not ahead; running/spacing/retry; fetch error once. All pass.
- `npm run check` is green except 2 timeouts in core publish.test.ts under full load. That file passes alone (11/11) and does not touch this change.
- I rewrote the topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md) for the new path.
- After the merge, an admin must press redeploy ONCE so the puller goes live. After that, the server pulls every merge itself.

## What I need from you
Nothing needed now. After the merge (next session), an admin presses redeploy once.
