---
id: "dc_7j4ar9jgty"
type: "report"
state: "building"
title: "One agent model, step 3 is live (PR #269, 6e6d663): agent status is one transition table, a dismissed agent can no longer be revived by stop → resume; step 2 (visitor desks) queued"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_dims7pqbeh","dc_txyovg40r3","dc_djha9wtjj7","dc_jjyo8ehufp"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Secretary\": No-go on visitor token accounting for gr_a5ct690l7a KR 2 (Mitchell, 1:1 mt_i50xwu4z2t at 18:16 UTC: \"i don't think we need to worry about accounting for visitor"
decidedBy: "ag_7tiwyqva83"
decidedAt: "2026-11-04T18:17:13.636Z"
sessionId: "se_7e0jq0zrs0"
createdAt: "2026-11-03T03:30:10.856Z"
updatedAt: "2026-11-04T18:17:13.636Z"
---
Live: 6e6d663 (ours), since /api/health startedAt 2026-11-03T03:27:30Z.

## Shipped
**1. One agent model, step 3: the agent status state machine**
**What it is:** Grant gr_a5ct690l7a, KR kr_p6nsa3zknw. PR #269 (merged as 6e6d663) puts every agent status move in one table, `STATUS_TRANSITIONS` (packages/schema/src/index.ts:492), enforced in `World.setStatus` (core/src/world.ts:366) with a 409 on any move outside it: retired is terminal, banned goes only to retired, stopped goes only to idle/offline/banned/retired. One `isGone` predicate replaces the inline retired/banned checks (43 lines → 5 across core, runtime, server, web); the budget sweep's SKIP_STATUSES is gone. `ops.stopAgent` (core/src/ops.ts:264) refuses a gone agent with 409 "X is retired.", which closes the live bug where dismiss → stop → resume revived a retired agent; meeting decisions and review-continue on a retired author no longer revive it either. 4 named tests in core/test/agent-lifecycle.test.ts and docs/invariants/agent-lifecycle.md (7 invariants, linked from AGENTS.md). Reports [dc_djha9wtjj7](2026-11-03-pr-269-ci-green-but-main-moved-3-times-re-merged-m-ha9wtjj7.md), [dc_txyovg40r3](2026-11-03-pr-269-merged-as-6e6d663-step-3-status-transition-yovg40r3.md), [dc_dims7pqbeh](2026-11-03-gr-a5ct690l7a-step-3-live-6e6d663-retired-fork-sta-ms7pqbeh.md).
**What you'd see:** API-only. Signed in as admin, click Stop on a retired fork (any entry under GET /api/agents/ag_croreod6q3/forks → retired) and you get 409 "… is retired."; Resume leaves it retired. Verified live by a fork with a resident token: its stop and resume calls got 403 (permission is checked before the gone check, the right order) and the fork ag_yapnp29vj9 stayed retired (read 2026-11-03T03:28:02Z). CI: PR run 41571346534 green; main's own run on 6e6d663 was concurrency-cancelled by the next push, the run on df1cb9e was still in progress at 03:28.
**Your call:** Mark kr_p6nsa3zknw (and kr_lrjhxy0pea from the last rollup) met on the grant if the live checks satisfy you.

Queued now: step 2 (KR kr_ie3i3swby4, as_c2iiep5v5e): a visitor registers on a goal and gets a desk beyond headcount that never counts as a fork slot and is not Bank-metered. If that needs Bank/token-accounting code, the fork stops that part and I bring you the exact lines.

## Decided
- [dc_dims7pqbeh](2026-11-03-gr-a5ct690l7a-step-3-live-6e6d663-retired-fork-sta-ms7pqbeh.md) → approve (step 3 verified live; step 2 queued)
- [dc_txyovg40r3](2026-11-03-pr-269-merged-as-6e6d663-step-3-status-transition-yovg40r3.md) → approve (PR #269 merged as 6e6d663 after two clean re-merges of main; a red deadcode on main fixed on the branch)
- [dc_djha9wtjj7](2026-11-03-pr-269-ci-green-but-main-moved-3-times-re-merged-m-ha9wtjj7.md) → approve (main moved 3× during the merge; re-merged to 15159e10, PR marked ready)
- [dc_jjyo8ehufp](2026-11-03-exploration-main-went-red-10-times-in-6-days-and-t-yo8ehufp.md) → approve (red-main exploration findings [dc_pifcrlzdg9](../../note/2026-11/2026-11-03-red-main-2026-10-28-11-02-10-red-episodes-causes-a-fcrlzdg9.md): 22 red main runs in 10 episodes over 6 days; proposal filed, in your in-tray)

## Key results
Grant gr_a5ct690l7a "One agent model" (funded 1,000,000; 631,112 spent at the last rollup + 36,616 + 27,975 for the two merge sessions + the live-check session, so roughly 700k):

| Key result | Status | Evidence |
|---|---|---|
| kr_lrjhxy0pea moderator, reviewer, residents list, Ada gone (due 11-07) | at-risk in the town; live since 024b236 | /api/town no Ada, /api/roles no moderator/reviewer ([dc_cuygorz7ae](2026-11-02-one-agent-model-ada-moderator-and-reviewer-roles-a-ygorz7ae.md)) |
| kr_p6nsa3zknw status transition table + isGone + stop guard (due 11-07) | not-started in the town; LIVE since 6e6d663 | STATUS_TRANSITIONS in schema, 4 tests in core/test/agent-lifecycle.test.ts pass in CI, stop on a retired agent → 409 (ops.ts:264) |
| kr_ie3i3swby4 visitor desk beyond headcount (due 11-07) | not-started; queued as_c2iiep5v5e | — |
| kr_8a7vskwse2 adopt verb for a goal with no desks (due 11-10) | not-started | last; may become a follow-up grant per the stop condition |

Today's spend by lane: exploration 65,339 tokens (free under the goal: 0), directed 118 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_7op2v8fjcl), 1 request ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md)), 1 rollup ([dc_cuygorz7ae](2026-11-02-one-agent-model-ada-moderator-and-reviewer-roles-a-ygorz7ae.md))._
