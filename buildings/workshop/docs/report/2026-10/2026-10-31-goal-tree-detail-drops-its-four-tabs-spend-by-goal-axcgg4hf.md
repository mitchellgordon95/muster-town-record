---
id: "dc_4saxcgg4hf"
type: "report"
state: "building"
title: "Goal tree detail drops its four tabs; Spend by goal now lives in the Bank's Spending tab (PR #155 merged e97dd9c, redeploy queued)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_hsq0e5a587","dc_jy52erwf1w"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/155"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #155 merged e97dd9c; live check as_jp4sfenvfo waits on deploy e97dd9c. Rollup 34 Shipped item."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:01:30.033Z"
sessionId: "se_2idcolklgl"
assignmentId: "as_n0aqnm802e"
costUsd: 5.751152749999999
tokens: 115023
turns: 58
createdAt: "2026-10-31T05:01:05.087Z"
updatedAt: "2026-10-31T05:01:30.033Z"
---
## What I did
Built mt_n25udpflus decision 5 myself (one focused change). PR https://github.com/mitchellgordon95/muster-town/pull/155, merged into main as **e97dd9c**; redeploy queued ~05:05Z; live check as_jp4sfenvfo queued, waiting on deploy e97dd9c (directed, sourceId mt_n25udpflus, page [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md)).

## Findings
- **Goal tree detail**: the History, Subtree, Spend and Queue tabs and their components are gone from `GoalTreePanel.tsx`; the detail now ends at the key result cards (Pix 3's desk line from PR #156 kept).
- **Spend by goal**: a new section on the Bank's Spending tab (`GoalSpend.tsx`, renamed from `GoalSpendTab.tsx`): a goal picker (root by default) over the same `GET /api/goals/:id/spend`, with the 7/30/90-day window and "Funded by me". The Bank's room and tab list are unchanged (no new station).
- **Queue**: only on building panels; `QueueTab` takes a building id, the lane-title button went. `GET /api/goals/:id/queue` stays for agents.
- **History**: out of the web entirely, no "last changed" line; `GET /api/goals/:id/history` stays for agents (the Planner's digest). The web API client lost `goalHistory` and `goalQueue`.
- Docs updated: docs/goals.md (editor section, "Spend by goal", Kanban "Where", the UI table), docs/architecture.md, docs/bank.md, code comments in core; docs/log.md line added. No migration, no Bank booking change.
- Verification: `npm run check -- --fast` green before the merges (docs, typecheck, 111 web + affected core/server tests); after merging main twice (PR #154 cards/retire confirm, PR #156 desks per goal; both conflicts were only the import lines and the removed components) typecheck and all 183 web tests pass locally. CI passed on the first push (2m31s); the second merge commit was merged on the local checks before its own CI run finished, so the main-branch check is the proof for it. knip could not run on this desk (not installed; the pinned npx run showed only pre-existing unused exports, none new).
- Not yet live-checked: the live check fork will confirm the tab-free detail and Spend by goal on e97dd9c and take the crop for rollup 34.

## What I need from you
Nothing needed.
