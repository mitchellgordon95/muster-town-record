---
id: "dc_gwq0ilj2z1"
type: "report"
state: "building"
title: "Exploration: a non-admin captain sees rollups in Mine but can't decide them, open a 1:1 or plant a flag; proposed gr_zsm1piyqyx (180k)"
authorId: "ag_0r686saeph"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_tnuw3oeke2","dc_04i3sll7q5","dc_ivddd9lih7","gr_bwm0iz7rwl"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Findings dc_tnuw3oeke2 and topic page dc_ooe47kx4un cover it; gr_zsm1piyqyx reaches Mitchell through the Town Hall in-tray on its own. Funding wakes me with its first step. The open question (directed work bounded by a captain's subtree free tokens) goes in the rollup 37 \"Your call\" line for this item, not Needs."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:06:19.813Z"
sessionId: "se_y2k16g7sa9"
assignmentId: "as_foez6ya544"
costUsd: 1.1378209000000001
tokens: 56891
turns: 31
createdAt: "2026-11-01T02:05:24.672Z"
updatedAt: "2026-11-01T02:06:19.813Z"
---
## What I did
I checked which of the building goal's four steering channels (goals, grants, report review, meetings) a non-admin captain can use. I read the gates on main af85f2a and checked the live town at 7ca64bc (GET /api/goals, /api/meetings). I wrote up the findings in [dc_tnuw3oeke2](../../note/2026-11/2026-11-01-findings-a-non-admin-captain-can-be-routed-work-bu-uw3oeke2.md) and started a topic page, [dc_ooe47kx4un](../../wiki/2026-11/2026-11-01-captain-steering-rights-e47kx4un.md). I proposed one grant, gr_zsm1piyqyx. I skipped the visitor-agent direction because the A/B/C shape is still Mitchell's TODO ([dc_ivddd9lih7](../../wiki/2026-10/2026-10-28-visitor-agent-reports-ddd9lih7.md)).

## Findings
- **These work for a captain:** editing goals (goals.ts:156, `owns`) and funding, countering or rejecting grants (grants.ts:789 `canFund`).
- **These don't:**
  - **Deciding a Town Hall rollup.** Rollups are routed to the captain's Mine by the building's attachment, but `canDecide` requires `building.review` on the Town Hall (intray-routes.ts:36, ops.ts:198).
  - **Opening a 1:1 or meeting with a manager under their goal.** It requires `meeting.facilitate` or `building.review` on that building (meetings.ts:87,165; ops.ts:516/548).
  - **Planting a flag.** It requires `building.assign` (domain.ts plantFlag).
- **This matches the docs as written.** docs/goals.md "Captains on nodes" gives captains only goals.edit and funding, even though it says "an owner's reports are the managers of the buildings attached in their subtree".
- **Live:** no goal has a non-null ownerId at 7ca64bc, and all of the last 100 meetings are Mitchell's 1:1s. Nobody but Mitchell has steered yet.
- **Proposal gr_zsm1piyqyx (180,000 tokens):** one helper, `owns(attachmentOf(building))`, added beside each of those role checks, plus tests, the docs and the web buttons. Its key results are:
  - kr_f1wzp12vtr: a captain decides a rollup in their Mine.
  - kr_k2gesp1b5e: a captain opens a 1:1 and plants a flag inside their subtree, and gets 403 outside it.
  - kr_xx9wtfnwh8: tests and docs cover the new rights.
  - It complements gr_bwm0iz7rwl (which makes a stranger a captain) and does not overlap it. There are no Bank or lane changes.
- **Open question, not in scope:** should directed work a captain starts be bounded by their subtree's free tokens? Today directed work bypasses grants (policy.ts).

## What I need from you
Decide gr_zsm1piyqyx in the Town Hall in-tray.
