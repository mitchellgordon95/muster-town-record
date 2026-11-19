---
id: "dc_8zvfwxreid"
type: "report"
state: "building"
title: "Proposed gr_rlt0ctnhqk: the town merges green PRs itself (36% of work sessions are merge-only)"
authorId: "ag_ha2kg9gf97"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration ended in proposal gr_rlt0ctnhqk (250k: M, S, S) with its ask card filed by Mara 1 at propose time; Mitchell decides it in the Town Hall in-tray. Findings dc_mozm3rwrza hold up against the code: pr-checks.ts polls each {pr: N} wait once a minute with the repo token and waits.ts ends the wait when checks finish, so a merge-when-green mode is a small extension. Nothing to queue until a decision lands."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-19T00:05:46.934Z"
sessionId: "se_ykt64pwrsc"
assignmentId: "as_trfjuamjs9"
costUsd: 1.7601517
tokens: 88008
turns: 34
createdAt: "2026-11-19T00:04:47.483Z"
updatedAt: "2026-11-19T00:05:46.934Z"
---
## What I did
I looked for toil the town could do instead of agents. I read CI history (100 main push runs, 300 PR runs) and the last 200 town sessions with their assignment titles. I wrote findings [dc_mozm3rwrza](../../note/2026-11/2026-11-19-findings-a-third-of-work-sessions-only-merge-a-gre-zm3rwrza.md) and proposed gr_rlt0ctnhqk (250k: steps M, S, S).

## Findings
- **Merge-only sessions:** 42 of 117 work sessions (36%) between 2026-11-16 18:15Z and 2026-11-19 00:00Z did only one thing: "if PR #N CI is green, mark ready and squash-merge". They cost 679,720 adjusted tokens, which is $13.59 of $100.98 list (13%). These sessions run in every building.
- The runtime already polls parked PRs' checks with the repo token (packages/runtime/src/pr-checks.ts). An opt-in `{pr: N, merge}` wait would let the town merge on green itself. Only red CI or a conflict would wake an agent.
- GitHub native auto-merge is not usable here: `allow_auto_merge` is false and there is no rulesets or required-check rule.
- **Leads dropped:**
  - Main CI: all 13 failures in 9 days were deploy jobs, none were code checks.
  - Timing flakes: about 1% of PR runs (3 of 300).
  - Most PR failures are knip unused exports. The pre-push hook (fixed in PR #499) already targets those under gr_baf19xtg7p.

## What I need from you
Fund, counter or reject gr_rlt0ctnhqk.
