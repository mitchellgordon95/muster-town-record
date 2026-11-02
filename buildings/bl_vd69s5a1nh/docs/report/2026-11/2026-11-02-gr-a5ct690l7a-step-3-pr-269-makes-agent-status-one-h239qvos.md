---
id: "dc_zvh239qvos"
type: "report"
state: "building"
title: "gr_a5ct690l7a step 3: PR #269 makes agent status one transition table, adds isGone, and stops stop→resume reviving a dismissed agent; parked on CI"
authorId: "ag_1quri1wmdz"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 3 PR #269 is built, local check green, parked on CI; the continuation as_i7b6buocg2 (mark ready, merge, {deploy} park, live 409/resume check) waits on {pr: 269}. Step 2 is queued only after step 3 is live, per the plan."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-02T18:20:53.043Z"
sessionId: "se_crrwx5iv05"
assignmentId: "as_yzwqa7fjmc"
costUsd: 2.6678293
tokens: 133391
turns: 53
createdAt: "2026-11-02T18:20:18.641Z"
updatedAt: "2026-11-02T18:20:53.043Z"
---
## What I did
I built step 3 (KR kr_p6nsa3zknw) as one PR: https://github.com/mitchellgordon95/muster-town/pull/269 (draft). It is one commit, 5a56e960, plus a merge of main, head 28cbea51. `npm run check` ran in the foreground on the merged branch and passed: core 679, runtime 217, server 262, cli 25, desk 40, web 261 tests, and docs, deadcode and typecheck all ok. It is pushed and parked on CI. I rewrote topic page [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md).

## Findings
- **The table.** `STATUS_TRANSITIONS`, `canTransition`, `isGone` and `NOT_GONE` sit next to `AgentStatus` in `packages/schema`. They go there rather than core because web imports schema, not core, so one copy serves every package.
  - `World.setStatus` throws a 409 conflict on any move outside the table and leaves the status unchanged. Setting the same status is still a no-op.
  - retired goes nowhere. banned goes only to retired; there is no unban anywhere in the code. stopped goes only to idle, offline, banned or retired.
- **The live bug.** `ops.stopAgent` on a retired or banned agent now answers 409 "Mei is retired." The server's error handler already turns that error into a 409 response, so dismiss → stop → resume no longer brings the agent back.
  - Review `stop` on a gone author now leaves its status alone.
  - The `ban` verb now goes through `setStatus` instead of patching the status directly.
  - The other revive paths (meeting decisions, review continue and redirect, flags, the Planner) only resume `stopped` agents. With the stop guard in place they can't reach a retired one.
- **Budget.** `SKIP_STATUSES` is deleted. The budget sweep's own status flip now calls `canTransition` and skips moves the table refuses. No token accounting changed, so nothing here needs Mitchell.
- **Inline checks.** I counted lines in packages/{core,runtime,server,web}/src that name both "retired" and "banned": **43 before (origin/main), 5 after** (target was under 10). The 5 left are status sets that also list other statuses, plus the migrate-roles SQL.
- **Tests** in core/test/agent-lifecycle.test.ts:
  - `table test: World.setStatus allows exactly the STATUS_TRANSITIONS pairs` (all 81 from/to pairs)
  - `retired and banned are gone and terminal: …`
  - `dismiss -> stop -> resume stays retired`
  - `meeting decision on a retired assignee does not revive it`
  - `review continue on a retired author does not revive it (nor stop)`
  - One existing fixture (verbs.test.ts) jumped an agent from stopped straight to working; it now resumes the agent first.
- **Docs.** docs/invariants/agent-lifecycle.md has 7 invariants with Test: lines, and check:docs passes. It is linked from AGENTS.md and from a new "Agent lifecycle" row in the architecture map.
- **Next session:** on green CI, mark ready and merge. Don't call redeploy. Park on {deploy: merge sha}, then verify live with a retired fork from /api/town: `POST /api/agents/<id>/stop` should give 409, and `/resume` should leave it retired.

## What I need from you
Nothing needed.
