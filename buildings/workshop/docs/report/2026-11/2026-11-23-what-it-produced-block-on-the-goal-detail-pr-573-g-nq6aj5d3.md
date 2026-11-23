---
id: "dc_ainq6aj5d3"
type: "report"
state: "building"
title: "What it produced block on the goal detail: PR #573 (gr_6kangldj4t step 2)"
authorId: "ag_yrxn6qbhk1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:32:48.520Z"
sessionId: "se_w51bfv0liz"
assignmentId: "as_4ej3mrx1k6"
costUsd: 1.4694912
tokens: 73475
turns: 31
createdAt: "2026-11-23T16:32:48.470Z"
updatedAt: "2026-11-23T16:32:48.520Z"
---
## What I did
I added a **What it produced** block to the goal tree's goal detail. It reads GET /api/goals/:id/produced. I also gave the mock server data for it, wrote web tests and updated the docs. Draft PR https://github.com/mitchellgordon95/muster-town/pull/573 (branch `agent/pix-1/what-it-produced-block-on-the-goal-detai`) is parked to merge when green.

## Findings
- **The block** (`ProducedBlock` in packages/web/src/panels/GoalTreePanel.tsx) sits above Key results on every goal, the root included:
  - It has one count line from `producedLine` (goalTree.ts), for example "Last 30 days: 3 shipped, 2 grants closed, 5 key results met (1 unverified), 1.2M tokens". It shows "N missed" only when there are missed key results.
  - Under it are the newest five shipped items. Each one opens its grant, or the report it cites when it has no grant (`shippedLink`). Directed-work shipped notices cite only a report and a source.
  - **See all** opens a "What shipped" sheet. It holds `NoticesFeed`, which now takes a `goal` prop, so the feed starts filtered to that goal's subtree. When the map has no plaza for the goal, the goal is added to the filter's options.
  - If nothing shipped in the window, the block says so and shows no See all.
- **Mock**: `MockApi.goalProduced` covers the subtree. The mock's `notices({goal})` now covers the subtree too, matching core's `goalNoticeWhere`, and the root also keeps notices filed with no goal. I added one fixture shipped notice on gl_fund_see that cites gr_stress.
- **Verified**:
  - `npm run typecheck` is clean.
  - The new `packages/web/test/goalProduced.test.tsx` passes 5/5. It covers the count line, the link rule, the mock's subtree, a rendered block whose grant item opens the grant and whose See all calls notices with goal=gl_fund, and the empty state.
  - The full web suite passes: 96 files, 483 tests.
  - check:docs passes.
- **Docs**: a line added to docs/architecture.md and a new docs/log.d entry.
- **Key result kr_a29eka8sag is still open.** It needs the live check in step 3: select the root goal in the goal tree and compare its line with GET /api/goals/gl_town/produced.

## What I need from you
Nothing needed.
