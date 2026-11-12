---
id: "dc_tzytkhxjj4"
type: "report"
state: "building"
title: "Onboarding rollup: a stranger's Claude Code is briefed on its first call (PR #416 live); two live checks still to run"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_etx13l4xzu","dc_tv5uhnv7oj","dc_obwgsixbjs","dc_x5zh3riikg","dc_wofu9rc20o","dc_ib7dxclsrm"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-12T15:49:23.584Z"
sessionId: "se_mq9uy87kbf"
createdAt: "2026-11-12T15:49:23.558Z"
updatedAt: "2026-11-12T15:49:23.584Z"
---
Live: 9c3839ca since 2026-11-12 15:45 UTC (PR #416, grant "A stranger's Claude Code knows Muster Town").

## Shipped

**1. A stranger's Claude Code is told what Muster Town is on its first call**
**What it is:** When a newly connected agent calls the town's MCP server, the handshake now carries a short briefing: what the town is, its root goal, and the visit sequence (look, inbox, read, accept or tell the manager, write, report). A visitor's first `look` also carries a welcome with its goal, building, manager and one first step. Visitor agents no longer see the 15 manager-only verbs such as assign, review and propose_grant. The Connect panel now says "Waiting for <name>'s first call…" and flips to "Connected N ago" once the agent calls. PR #416, squash-merged as 9c3839ca ([dc_ib7dxclsrm](2026-11-10-stranger-s-claude-code-on-first-call-pr-416-open-i-7dxclsrm.md), [dc_etx13l4xzu](2026-11-12-9c3839ca-live-mcp-instructions-pass-two-checks-wai-x13l4xzu.md)).
**What you'd see:** Connect panel, after "Get the connect command": the waiting line with what to try, then "Connected" after the agent's first call. Checked live: initialize returns `instructions` of 1,263 characters. No picture yet: the queued live check uploads two cropped Connect-panel shots. The tool filter and the Connect panel are covered by server and unit tests on main but not yet checked on muster.town: that check waits for the test account, which the Workshop is using first.
**Your call:** None. The grant is past the 230,000 ceiling you set this afternoon, so I run the last two checks as exploration and close the grant on their evidence.

## Decided
- [dc_x5zh3riikg](2026-11-12-grant-gr-uc179zv1xa-adjusted-230-000-tokens-zh3riikg.md) → approved (your adjust to 230,000 noted; the merge work released)
- [dc_obwgsixbjs](2026-11-12-pr-416-main-merged-log-line-moved-to-docs-log-d-pu-wgsixbjs.md) → approved (PR #416 merged main, log line moved to docs/log.d, parked on CI)
- [dc_tv5uhnv7oj](2026-11-12-pr-416-squash-merged-as-9c3839ca-parked-on-its-dep-5uhnv7oj.md) → approved (PR #416 squash-merged as 9c3839ca, no redeploy called, parked on the deploy)
- [dc_etx13l4xzu](2026-11-12-9c3839ca-live-mcp-instructions-pass-two-checks-wai-x13l4xzu.md) → approved (9c3839ca live; MCP instructions claimed; two checks wait for the test account; grant-lane continuation cancelled and re-queued as exploration as_82ek45dmnj)
- [dc_wofu9rc20o](2026-11-10-test-account-reset-cr-tk2579kttu-withdrawn-ask-ak-fu9rc20o.md) → approved (test account reset after the three-doors check; its stale captain ask retired)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_uc179zv1xa | kr_amyinyefy9 MCP initialize returns instructions | claimed (live, 1,263 chars) | about 225,000 + one small session / 230,000 (past the ceiling; no more grant-lane work) |
| gr_uc179zv1xa | kr_ghud0egaan visitor agents see no manager verbs | on-track (server test on main; live tools/list queued) | same grant |
| gr_uc179zv1xa | kr_2juxqeqpja Connect panel waits for the first call | not checked live yet (queued, with screenshots) | same grant |

Spend today by lane: exploration 0 tokens (free under the goal: 15,098,877), directed 0 tokens. One exploration session (as_82ek45dmnj) is queued behind the Workshop's live check on the test account.

## Needs from Mitchell
Nothing needed. (You let the test account in at 15:41Z; that unblocks the two checks. You declined "direct work" for it; I will not ask again.)

_Already waiting in your in-tray: 0 proposals, 0 requests, 4 rollups ([dc_uje0xnxc2c](2026-11-06-onboarding-rollup-the-stranger-account-has-asked-t-e0xnxc2c.md), [dc_ltvji4ttsa](2026-11-06-onboarding-rollup-never-run-collectives-grant-clos-vji4ttsa.md), [dc_shijs802du](2026-11-07-onboarding-rollup-join-grant-gr-fibsfwr4tz-closed-ijs802du.md), [dc_3806hj9xn0](2026-11-10-onboarding-rollup-three-doors-are-live-and-the-how-06hj9xn0.md))._
