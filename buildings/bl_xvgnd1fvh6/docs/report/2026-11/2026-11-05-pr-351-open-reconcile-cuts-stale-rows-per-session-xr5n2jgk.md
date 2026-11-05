---
id: "dc_5pxr5n2jgk"
type: "report"
state: "building"
title: "PR #351 open: reconcile cuts stale rows per session, not per agent; parked on CI"
authorId: "ag_yxnpme1s0v"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #351 (reconcile cuts stale rows per session, not per agent) is parked on CI; its continuation as_kf59hpu9p7 waits on {pr: 351} and will mark ready + merge on green. Live check falls to sc_ul1b1ntqik (no agent with two running manage rows after a restart). No rollup now: nothing new is live since rollup #39."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-05T05:25:34.173Z"
sessionId: "se_7itisbn97i"
assignmentId: "as_2wkjp874mx"
costUsd: 0.4840900999999999
tokens: 24205
turns: 12
createdAt: "2026-11-05T05:25:26.462Z"
updatedAt: "2026-11-05T05:25:34.173Z"
---
## What I did
Changed `Ops.reconcile` to take live **session** ids (packages/core/src/ops.ts) and the runtime to pass `[...ctx.live.values()].map(l => l.sessionId)` (packages/runtime/src/index.ts:274). Updated the doc comment and the existing v12 reconcile test, and added a test: one agent with an adopted running desk work session plus a stale running manage session. After reconcile, the manage row ends `interrupted` "cut by restart". The work row and its assignment stay running/active, and the body stays `working`. Draft PR https://github.com/mitchellgordon95/muster-town/pull/351 (commit on branch agent/cleo-1/reconcile-per-session-not-per-agent-a-st).

## Findings
- Every caller of `reconcile(` checked. Only the runtime passes ids. The other tests call `reconcile([])` or `reconcile()`, so they behave the same.
- The requeue and body-status passes re-query running sessions after the cut, so they still work. The new test confirms it.
- Typecheck is green. These suites pass locally: core v12, visitors and walk-home (25 tests); runtime one-on-one, running-debit and redeploy (43); runtime adopt, forks and v12 (23).
- Still to do when this resumes: mark the PR ready, merge it once CI is green, and record the merge sha. Checking it on the live server needs a restart after the deploy. If none happens in that session, the daily sc_ul1b1ntqik check covers it: no agent should have two `running` manage rows after a restart.

## What I need from you
Nothing needed.
