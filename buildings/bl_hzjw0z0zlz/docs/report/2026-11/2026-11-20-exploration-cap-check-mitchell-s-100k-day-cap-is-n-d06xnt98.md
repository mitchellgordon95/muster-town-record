---
id: "dc_9jd06xnt98"
type: "report"
state: "building"
title: "Exploration cap check: Mitchell's 100k/day cap is NOT set on the Onboarding goal; today's explore spend is 75,266 in 2 runs"
authorId: "ag_osknycdlfr"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Passed up to the humans as ask ak_52xdmgycz5: Check done: the cap Mitchell chose on ak_twfr93gbix is not on the goal (exploreCapTokensPerDay null, no goal.edited event). Only an admin or the goal's captain can set it (goals.ts:301-307; GoalTreePanel.tsx:314-321 is the Save button). Passing it up as one click ask."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-20T18:25:10.016Z"
sessionId: "se_925v43cc1a"
assignmentId: "as_gpovegk9qp"
costUsd: 0.5612604
tokens: 28063
turns: 13
createdAt: "2026-11-20T18:24:00.435Z"
updatedAt: "2026-11-20T18:25:10.016Z"
---
## What I did
Read-only check, no code. Read live GET /api/goals/gl_bl_hzjw0z0zlz (and its parents), /api/goals/gl_bl_hzjw0z0zlz/history, /api/health budgets (server time 2026-11-20T18:23:23Z, commit ed3c88f1), /api/sessions, and Kelly's log.

## Findings
- **Cap not set.** gl_bl_hzjw0z0zlz has `exploreCapTokensPerDay: null` (inherited), last edited 2026-11-01T02:18:50Z. Its parent gl_trust is also null. The cap that applies comes from gl_town: 500,000 tokens/day (set 2026-11-17T03:26Z). /api/health shows the same for Onboarding: cap 500,000/day on gl_town, 481,482 used town-wide today.
- **No edit event.** The goal's history has no `goal.edited` "Exploration cap on…" entry. The newest entry is from 2026-10-26. So nobody set a cap after Mitchell's 18:21Z decision on ak_twfr93gbix.
- **Spend today (2026-11-20, server day).** Onboarding exploration is 75,266 adjusted tokens (/api/health). That matches 2 runs in Kelly's log: as_yb8xpbxqbg, the explore tick, done 00:03Z at 13,332, and as_2g87ovym8j, the PR #531 review, done 01:56Z at 61,934. Since the decision there is 1 run, this check (as_gpovegk9qp, running).
- **The loop is quiet today.** No empty explore tick has run since 00:03Z. On 2026-11-19 the ticks ran every 30 min at about 10.6k–11k each. So the "about 300k a day" premise is out of date today, though the loop can start again. Without the cap, the only limit is gl_town's 500k, and the town is at 481k of that.
- Note: /api/sessions?agentId only shows a fork's current incarnation, so I took the per-run figures from Kelly's log. Their sum matches the health figure exactly.

## What I need from you
Mitchell: set exploreCapTokensPerDay = 100,000 on the Onboarding goal ("Minimize confusion when joining a Muster Town through UX design") in the goal tree. Clicking the ask recorded the decision only, so the cap is still not set.
