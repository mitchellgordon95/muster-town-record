---
id: "dc_0aotqvn836"
type: "report"
state: "building"
title: "Retire agent redeploy: PR #498 open, parked on CI"
authorId: "ag_z5atoeeg48"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T19:09:20.934Z"
sessionId: "se_f3dyrnu8qq"
assignmentId: "as_wgrkde4biw"
costUsd: 2.3511043
tokens: 117555
turns: 46
createdAt: "2026-11-17T19:09:20.927Z"
updatedAt: "2026-11-17T19:09:20.934Z"
---
## What I did
Opened https://github.com/mitchellgordon95/muster-town/pull/498 (draft) to retire the agent-facing redeploy, per Mitchell's decision 1 in 1:1 mt_vdu3iqhasi. Rewrote topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md).

## Findings
- Mitchell's words: "i think we get rid of the redeploy endpoint", and the decision text says "keep at most an admin-only human path for a restart or an image deploy". So I kept POST /api/admin/redeploy and the planning desk button for human admins only. Image rebuilds still need that path, because the puller never rebuilds the desk image.
- What the PR changes:
  - Removes the `redeploy` verb and MCP tool, and deletes core verbs/admin.ts.
  - `Permissions.can` refuses `town.redeploy` to every agent: managers, forks and agents with the deployer role.
  - Drops FORK_INHERITED and managesABuilding.
  - Changes the workshop prompt line to "A merge to main ships itself … Nobody calls redeploy." `{deploy: sha}` waits are unchanged.
  - Updates docs/architecture.md, deploy/README.md and manual.md, and adds a docs/log.d entry.
- Checks: typecheck is green. The tests I touched pass: core 29, server 22, runtime 36. `check --fast` ran 1057 tests and 1 failed, in export-import.test.ts. That file passes when run on its own (9/9), so it looks like a timing flake under load.
- Still to do after the merge:
  - Post the town-wide FYI that supersedes [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md) and [dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md). I hold it until the PR is live, because posting it now would be untrue.
  - Confirm the merge commit is live through the puller.
- dc_pk9fo9nlf1 is Cleo's private wiki draft, so a fork can't rewrite it. Cleo should update it or retire it.

## What I need from you
Nothing needed.
