---
id: "dc_n9b805a710"
type: "report"
state: "building"
title: "gr_a5ct690l7a: no visitor token counting, by Mitchell's word; Spend by goal now says a visitor's tokens are not tracked (PR #318, parked on CI; grant closes once it is live)"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_hwv38137vo","dc_87vz2ppews"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/318"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The work is parked on PR #318's CI and resumes by itself: merge, redeploy, close_grant gr_a5ct690l7a, then the rollup that says KR 2's visitor-token half was dropped on Mitchell's word. No separate assignment needed."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-04T18:27:28.945Z"
sessionId: "se_ma7lmnnmkj"
assignmentId: "as_xjth4zyf8u"
costUsd: 3.1051694500000004
tokens: 155258
turns: 29
createdAt: "2026-11-04T18:27:11.034Z"
updatedAt: "2026-11-04T18:27:28.945Z"
---
## What I did
Took Mitchell's no-go (1:1 mt_i50xwu4z2t, 18:16Z) as the decision: built no transcript upload, no self-report, no estimate of what a visitor spends. The only place the goal's page would have shown a visitor's tokens is the Bank's "Spend by goal" (GoalSpend.tsx; the goal editor itself shows no spend since 1:1 mt_n25udpflus decision 5), so that view now says plainly that a visitor's tokens are not tracked. Opened draft PR #318 (commit 08ec169) and parked on its CI.

## Findings
- **Change** (https://github.com/mitchellgordon95/muster-town/pull/318): schema `GoalSpend.visitors` (online visitors homed in the subtree's buildings; offline, retired, elsewhere and residents not counted); core `goalSpend` counts them and books nothing for them; the web Spend by goal shows, when any: "N visitors at desks under this goal: what they spend is not tracked. A visitor works from its own client, so its tokens are unknown and in none of these figures." Mock server carries the field.
- **Docs**: docs/goals.md "Spend by goal" and docs/invariants/agent-lifecycle.md now state the rule with Mitchell's words and the test; docs/log.md line added.
- **Verified**: `npm run typecheck` green; core goals-step4.test.ts 7/7 (new: visitors counted, their spend not); web goalsStep4.test.tsx 7/7 (new: the line's wording, null with none); `npm run check:docs` green. Pitfall for forks: a desk checkout behind main's lockfile fails every test with `t.unwrap is not a function` (zod) until `npm install`.
- **Grant**: not closed this session on purpose. close_grant wants evidence a human can check live, and PR #318 is still in CI. Next session: merge (own green PR, rule [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md)), redeploy, close_grant gr_a5ct690l7a (about 280k unspent tokens back to the Bank), then roll up saying kr_ie3i3swby4's visitor-token half was dropped on Mitchell's word, not missed. Wiki pages [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md) and dc_cc2lnlvzwx say so.

## What I need from you
Nothing needed.
