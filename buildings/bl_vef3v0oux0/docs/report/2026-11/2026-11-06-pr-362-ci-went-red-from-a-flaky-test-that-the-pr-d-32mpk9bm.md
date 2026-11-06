---
id: "dc_r932mpk9bm"
type: "report"
state: "building"
title: "PR #362 CI went red from a flaky test that the PR doesn't touch; merged main in to re-run CI, parked"
authorId: "ag_zl74j46bj1"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The parked continuation as_j38vtm32v4 already waits on {pr: 362} and carries the plan (squash-merge if green, no redeploy, park on {deploy: sha}, live check + picture). If the mcp-proxy restart-timing test fails again, tell Prod it's flaky and push an empty commit, as planned."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-06T04:26:18.989Z"
sessionId: "se_r5mzcfmwot"
assignmentId: "as_2749zoek32"
costUsd: 0.3999863
tokens: 19999
turns: 9
createdAt: "2026-11-06T04:26:11.598Z"
updatedAt: "2026-11-06T04:26:18.989Z"
---
## What I did
- I checked CI on PR #362 (https://github.com/mitchellgordon95/muster-town/pull/362) at 87e91d1c. It was red. The only failing test is `packages/*/test/mcp-proxy.test.ts › desk MCP proxy: riding out a town restart › connection refused…` (×, 5,264 ms). It is a restart-timing test, and the PR doesn't touch the MCP proxy (its 13 files are all finance). All the other test files passed (130 + 33 + 36 + 2 + 4).
- I couldn't rerun the failed job because the agent token was refused ("Resource not accessible by personal access token"). Instead I merged origin/main (31f1cc54) into the PR branch, which merged cleanly. Typecheck passed, and I pushed **d15900ab** to start a fresh CI run.

## Findings
- #362 is not merged yet. Live is still 5dc50c70, and kr_avafh64h02 stays on-track.
- Next session:
  - If CI is green: squash-merge without calling redeploy, park on {deploy: sha}, then do the live check. That means a picture signed out at 1400×900, today's numbers for Bank Transparency and Town Workshop, check:finance all ✓, and rewriting [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md).
  - If the same mcp-proxy test fails again: tell Prod/Workshop it's flaky, and push an empty commit to get another run.

## What I need from you
Nothing needed.
