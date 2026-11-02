---
id: "dc_teavwzh3fl"
type: "report"
state: "building"
title: "Explore: captains have no spending ceiling; proposed gr_kph1zjjrzg (captain budgets + tightest exploration cap)"
authorId: "ag_wpolpclefp"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_7yr1fea9lc","dc_zcuri3xdk2"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. gr_kph1zjjrzg is in the Town Hall in-tray and reaches Mitchell on its own; nothing queued until he decides. Findings dc_7yr1fea9lc stand as the record."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:06:18.521Z"
sessionId: "se_fg3216sl8p"
assignmentId: "as_uq4on1j8jq"
costUsd: 0.8379879000000001
tokens: 41899
turns: 19
createdAt: "2026-11-02T03:05:15.868Z"
updatedAt: "2026-11-02T03:06:18.521Z"
---
## What I did
I read the captain, grant-funding and exploration-cap code at main fbdec57, checked the live goal tree (live f1bf4c1, health read 03:04:15Z), wrote up the findings in [dc_7yr1fea9lc](../../note/2026-11/2026-11-02-findings-a-non-admin-captain-can-commit-the-shared-r1fea9lc.md) and filed one grant proposal, gr_kph1zjjrzg (ask 300,000 tokens, 3 key results due 11-06 and 11-07).

## Findings
- **A captain can fund without limit.** `Grants.canFund` lets a goal's captain fund grants anywhere in their subtree. Since f1bf4c1 (mt_fgsticyyhr), funding is never refused: any shortfall is just shown as overdrawn. So a captain who isn't an admin can commit any amount from the shared Bank.
- **A captain can raise the exploration cap set above them.** `exploreCapAt` uses the nearest cap up the tree, not the tightest one. A captain who sets a large cap on their own goal overrides the root's 500,000/day for their whole subtree.
- **No harm yet.** Mitchell captains every node in the live tree. But "Ask to captain" (gr_bwm0iz7rwl) and captains steering their buildings (gr_zsm1piyqyx, funded today) are exactly how a stranger becomes a captain.
- **What the proposal does:** adds a monthly budget per captained goal, set by the captain above or an admin. A captain below can't fund past that budget, but admins and captains higher up stay ungated, as Mitchell decided in mt_fgsticyyhr. Exploration caps would combine as the tightest on the path. The goal's detail would show how much of the budget is used. None of this is built; it's a proposal only.

## What I need from you
Fund, counter or reject gr_kph1zjjrzg. It changes token accounting, so it needs your decision. Two choices come with it: the default budget for a new captain (proposed 0) and the budget period (proposed a UTC calendar month).
