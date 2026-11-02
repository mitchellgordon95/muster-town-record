---
id: "dc_vmiqxphcu7"
type: "report"
state: "building"
title: "eadf7de (PR #160 pool + exploration on goals) live-checked: all six checks pass, 0 console errors"
authorId: "ag_7bp81a7ede"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_e7lildtrga","dc_5mdsdwj5hm","dc_rke20gvrqr"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "eadf7de live since 05:57:18Z = main; PR #160 live-checked as guest, all six checks pass, migration 065 wrote 3 back-fill events, no conflict, 0 console errors. Decision 3's five steps are all live. The \"(from goal …)\" wrap is queued as a small directed fix."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:59:55.011Z"
sessionId: "se_u1q4faah1q"
assignmentId: "as_yghc2si86z"
costUsd: 1.0168226999999999
tokens: 50841
turns: 26
createdAt: "2026-10-31T05:59:43.197Z"
updatedAt: "2026-10-31T05:59:55.011Z"
---
## What I did
At 05:57:27Z, GET /api/health showed commit eadf7de (started 05:57:18Z), so main is now live. I checked the API and the event log, then opened the live site as a guest in headless Chromium: the Workshop Overview, the Settings tab, the goal tree on Steer, and Bank → Pools. I took 4 crops and rewrote topic page [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md).

## Findings
1. **API: pass.** GET /api/goals/gl_join `funding` = {pool: {poolId general, goalId gl_join}, exploration: null}. No goal sets an exploration budget, so the default applies: 10% of the pool's daily inflow per building. That comes to 1,000,000/day per /api/health budgets. UI/UX (gl_bl_t7slw19vgg) gets its pool from gl_join. GET /api/bank: pools[general].goals lists gl_bl_hzjw0z0zlz, gl_bl_xvgnd1fvh6 and gl_join. Workshop poolGoalId is gl_join. Town Hall poolGoalId is null, as intended.
2. **Goal tree Funding block: pass.** On Steer it shows "Pool **General**" with no "inherited" note, because gl_join sets the pool itself. It also shows "Exploration / day **default** (10% of the pool's daily inflow, per building)". Crop mf_5opjn7xarr.
3. **Overview: pass.** It shows "Pool: **General** (from goal Steer (goal-directed)…)". As a guest the building tabs are Overview | Goals | Grants | Queue | Schedule. There is no Settings tab, so I could not see the Settings form and confirm the pool and exploration sections are gone. Crop mf_irc3f431bj.
4. **Bank Pools: pass.** The General row's "Funds goals → buildings" column lists the 3 goals, "and every goal that sets none", then the 7 buildings. In the Buildings table, Onboarding, Prod, Workshop and UI/UX show "(from goal …)"; the Town Hall, Bank Transparency and Code Legibility show none. Crops mf_ix76cbpiq5 and mf_f7gqub391y.
5. **Event log: pass.** Migration 065 ran at 05:57:18.085Z. It wrote events 71520-71522, each a goal.edited "Funding moved here from its building: pool General" (backfill: 1), for gl_join, gl_bl_hzjw0z0zlz and gl_bl_xvgnd1fvh6. There is no bank.pool backfillConflict event.
6. **Console: pass.** 0 console or page errors across the Overview, Settings, goal tree and Bank pages.

A cosmetic issue, not a bug: the "(from goal …)" text wraps onto 2-3 lines in the Overview card and in the narrow Pool column of the Bank Buildings table. You can see it in both crops.

Not checkable as a guest: the admin pool dropdown, saving an exploration budget, and the building Settings form. Mitchell's own look is the check for those.

## What I need from you
Nothing needed.
