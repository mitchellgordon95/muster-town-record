---
id: "dc_byen3segdt"
type: "report"
state: "building"
title: "Kelly 1's FYI (Dashboard removed in 7ad702d) acknowledged: nothing in Workshop code or docs still points at it; PR #238's merge conflict traced to it and Pix 1 told the resolution"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["ms_tvfedcggws","mt_ec2b7x80rg","dc_72nexb0bwn"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Kelly 1's FYI acknowledged; no Workshop code or docs point at the Dashboard; #238's conflict resolution told to Pix 1. Onboarding's shipped item, not ours. Done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T01:45:48.305Z"
sessionId: "se_tiblmaxbwk"
assignmentId: "as_xx3fi6dtl6"
costUsd: 1.73112695
tokens: 86556
turns: 15
createdAt: "2026-11-01T01:43:58.241Z"
updatedAt: "2026-11-01T01:45:48.305Z"
---
## What I did
Read Kelly 1's relay for Mitchell (ms_tvfedcggws): 7ad702d on main removes the Dashboard page (HUD ▤, DashboardPanel, KPI tiles, GET /api/kpis, core kpis.ts) per 1:1 mt_ec2b7x80rg decision 1. Checked the commit on origin/main, the live commit, leftover references in packages and docs, and the two open Workshop PRs against the new main. Replied to Kelly 1 (ms_wbheirkrnx; Kelly 1 was idle, so the town queued it to Kelly as as_hdj4sjctfq). Rewrote topic page [dc_72nexb0bwn](../../wiki/2026-10/2026-10-28-objectives-key-results-and-kpis-code-nexb0bwn.md) ("Objectives, key results and KPIs (code)") so it no longer lists GET /api/kpis or the Dashboard. Logged.

## Findings
- 7ad702d is on main (Kelly 1, 01:41:49Z) but not live: GET /api/health at 01:42:25Z still 139f587 (the redeploy for d9f28c5 is queued ahead of it). Kept, as the FYI says: the kpis table and migration 043, objectives and set_objective, GET /api/join-funnel.
- No Workshop code or doc on main still points at the Dashboard or GET /api/kpis (git grep over packages and docs: only the updated docs/goals.md and goal-directed-budgets.md rows, docs/log.md history, and the post-mortem's mention of the old route's cost).
- Knock-on: PR #238 (retainers, head a17921d) now conflicts with main at packages/web/src/api.ts (the type import line: main drops KpiKey/KpiView, #238 renames Schedule → ScheduleView) and docs/log.md. Pix 1 (as_kx9lt741qr) had already seen mergeable CONFLICT and was merging main into the branch when I looked; I told it the exact resolution (ms_2jl0kl7m2w). PR #236 (Planner revive, 8068e8c) merges clean with main; its CI check is in progress.
- Not a Workshop rollup item: the removal is Onboarding's shipped work (Kelly's rollup). [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) (Rollup 37 materials) has no Dashboard mentions; nothing to change there.

## What I need from you
Nothing needed.
