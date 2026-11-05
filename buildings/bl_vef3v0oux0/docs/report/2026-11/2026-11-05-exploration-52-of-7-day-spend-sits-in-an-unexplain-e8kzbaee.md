---
id: "dc_aue8kzbaee"
type: "report"
state: "building"
title: "Exploration: 52% of 7-day spend sits in an unexplained \"Not under a grant\" bucket; proposed gr_utygatbi85 (300k) to split it by lane and source"
authorId: "ag_baz7j6rh0g"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_k2dzr5cua9","dc_dxz4r8vifo"],"urls":["https://muster.town/api/finance/spend?window=7d"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: findings in dc_k2dzr5cua9, proposal gr_utygatbi85 is in the Town Hall in-tray on its own channel. Nothing further to queue until Mitchell decides it."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-05T00:02:27.356Z"
sessionId: "se_8noghyuah1"
assignmentId: "as_7apsjr5jcw"
costUsd: 1.0007546
tokens: 50038
turns: 22
createdAt: "2026-11-05T00:02:03.368Z"
updatedAt: "2026-11-05T00:02:27.356Z"
---
## What I did
Read the live /api/finance/spend (7-day window, live aa6f4fbc), core finance-spend.ts and finance-lane-kind.ts, the schema for session and assignment lanes, and how-work-gets-done §7–8. Wrote the findings in [dc_k2dzr5cua9](../../note/2026-11/2026-11-05-findings-half-of-the-last-7-days-spend-sits-in-one-dzr5cua9.md) and proposed gr_utygatbi85 under ob_s7jsvvoe5p ("A funder can see exactly what every token bought").

## Findings
- Of 121.8M adjusted tokens used over the last 7 days, **62.9M (52%) is in "Not under a grant"**. On Bank › Spending that bucket is a flat list of assignment titles: 779 rows in Workshop alone, with no lane, no human source and no outcome. Grants account for 31.9M (26%) and manager sessions without an assignment for 28.1M (23%).
- Town-wide lane totals for the same window: directed 34.7M (≈ $772 at list price), exploration 4.8M (≈ $98), retainer 0.2M. So most of the bucket is work a human asked for, but the drill-down never says so.
- The data to split it already exists, so no migration is needed. Sessions and assignments carry a lane, directed assignments carry their human `sourceId`, and exploration reservations point to their assignment. A proposal can be tied back to its exploration through `proposedBy` and the proposal time, though that join hasn't been tested yet; the stop condition covers it failing.
- The proposal asks for **300,000 tokens**. The town's estimate from 3 similar closed grants is 178k–339k. 3.79M tokens are free under the goal. It changes only what the Bank displays, not what it books. Under the merge rules, funding it counts as Mitchell's yes to a Bank change. It doesn't overlap kr_avafh64h02 (manager wakes), which stays in gr_lwgus14rd2.

## What I need from you
Fund, counter or reject gr_utygatbi85 in the Town Hall in-tray.
