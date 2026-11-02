---
id: "dc_nkdoluege5"
type: "report"
state: "building"
title: "Overview card: owner shown once, Grants line calls out funded grants outside the goal (PR #159, 9253c18, redeploy queued)"
authorId: "ag_awe2xvqvgb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. PR #159 (9253c18) merged, redeploy queued; a directed live check of 9253c18 is queued separately. The two funded grants naming key results outside Steer (gr_tvt32g9xly, gr_iq5m7dug56) go to rollup 34's Needs as a question for Mitchell."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:33:49.568Z"
sessionId: "se_ab6hthz14q"
assignmentId: "as_9xt89iqsts"
costUsd: 1.4932737999999999
tokens: 74664
turns: 50
createdAt: "2026-10-31T05:33:39.876Z"
updatedAt: "2026-10-31T05:33:49.568Z"
---
## What I did
Fixed both Overview oddities from [dc_k36sppoy2k](2026-10-31-c899aa8-live-checked-overview-card-map-banner-plan-6sppoy2k.md) in one PR: https://github.com/mitchellgordon95/muster-town/pull/159. It is merged as **9253c18** (after merging main, PR #158) and a redeploy is queued. I have not checked it live. `npm run check` passed (docs, deadcode, typecheck, tests; 186 web tests after the merge). GitHub reported no CI checks on the PR, so I merged on the clean merge state and the local check. The new unit tests cover the Grants line wording.

## Findings
- **Oddity 1 (repeated goal):** "Reports to the town admins via Steer…" is now **"Owner: the town admins · in the goal tree →"** (`GoalOwner` in BuildingPanel.tsx). The goal text now appears only once, in the card. docs/goals.md line 120 is updated to match.
- **Oddity 2 (0 funded vs 2 funded):** neither archived key results nor a counting bug caused this.
  - The Goals line (`goalsSummary`) counts funded key results in the building's own goal tree. That is 0 out of 9.
  - The Grants line counts every funded grant the building holds. The Workshop's two funded grants name key results under **other pillars**:
    - gr_tvt32g9xly → kr_6f9c200vsx under gl_fund
    - gr_iq5m7dug56 → kr_vyrhhiyotb under gl_trust
  - Both were funded before the Workshop was attached to gl_join.
  - The Grants line now labels this. Live data, rendered locally: **"Grants: 0 proposals, 2 funded (all on key results outside this goal), 4 closed or held"**.
  - Crops of the live Workshop data: before mf_hwb6ocvspz, after mf_sua82and3b. Both are ≤200 px tall.
- **Oddity 3:** this is not a bug. The planning desk labels the Town Hall row "Town Hall" on purpose: `PlanningPanel.tsx:44` checks the building kind, and the Town Hall has no goal path to show.
- Topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) is updated with the new state and the method for rendering a local page against live data.

## What I need from you
Nothing needed. One open question for whoever owns gr_tvt32g9xly and gr_iq5m7dug56: those two grants still name key results outside the Workshop's goal. The label is accurate, but someone may want to move or close them.
