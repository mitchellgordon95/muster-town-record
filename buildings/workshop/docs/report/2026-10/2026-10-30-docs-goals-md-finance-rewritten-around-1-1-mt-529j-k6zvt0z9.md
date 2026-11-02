---
id: "dc_vhk6zvt0z9"
type: "report"
state: "building"
title: "docs/goals.md finance rewritten around 1:1 mt_529jbnwvmi decision 1; PR #116 head 4af1ee1 (not merged)"
authorId: "ag_5vt79zkqot"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_529jbnwvmi","dc_0xqyrevla1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/116"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: docs-only rewrite on the PR #116 branch (4af1ee1, not merged), as decision 1 of mt_529jbnwvmi asked. Mitchell's read and his answers to the 7 remaining questions go in rollup 32's Shipped item / Needs, nowhere else."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T20:02:30.773Z"
sessionId: "se_xw6ihh0fqy"
assignmentId: "as_9srttx6zen"
costUsd: 0.9185099000000001
tokens: 45925
turns: 18
createdAt: "2026-10-30T20:02:08.836Z"
updatedAt: "2026-10-30T20:02:30.773Z"
---
## What I did
Read the mt_529jbnwvmi transcript and decision 1, then rewrote the finance parts of docs/goals.md on the PR #116 branch. Commit 4af1ee1 is pushed to agent/pix-2/design-doc-docs-goals-md-town-level-goal and I checked it is on origin. It is a docs-only change and is not merged. I also updated topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).

## Findings
- **New section "Finance: one balance, streams, desks"** replaces "Budget by node". It says:
  - There is no allocation by node and no budget tree. There is one balance, and pools go.
  - Human review of grants stays.
  - Steering is done with desks, with a caveat that a building on two subtrees shares its desks between them.
  - Streams and earmarks are paid in a draw order: the narrowest stream first, then the general balance. When an earmark runs dry, work carries on from the balance.
  - Free funds = balance + income for the week − remaining tokens on funded grants − open asks. This replaces the per-building `explorationTokensPerDay`.
  - A session uses one key, and only if that key covers the session's expected cost. Smaller streams build up until they do. The desk gets a cap.
  - Funders get a filter on the deck: key donors see exactly which sessions their key paid for, and money donors see their share pro rata. A held key is a secret: the donor sees its usage and can revoke it.
  - The Spend tab only reads subtree spend from session bookings.
- **"Expected session cost" uses real figures.** The last 89 finished work sessions (2026-10-29 20:50Z to 10-30 19:30Z) cost, in adjusted output tokens: p50 43k, p90 120k, max 337k. The doc proposes the building's 7-day p90 as the threshold.
- **Rest of the doc made consistent:**
  - The grant scope line, the reorg's "money moves", the lanes section (the per-building allowance is gone) and skip-level costs no longer mention pools.
  - "What changes" now says pools and the allowance go in steps 8 and 9.
  - The deck section has the funder filter.
- **Build order:**
  - Allocation by node is removed.
  - New step 8 is streams plus the draw order. New step 9 is the funder filter. Both are marked as Bank changes that need Mitchell's yes.
  - The Spend tab ships with step 3.
- **Open questions:** Q1 (who pays for Planner: there are no pools left to choose between) and Q9 (budget by node) are struck through as answered by mt_529jbnwvmi. 7 questions remain.
- One point the doc infers rather than taking from the meeting: a key whose own daily limit is below one session's cost can't be used on its own, and its donor is told so. It is marked in the doc as a rule to confirm.

## What I need from you
Mitchell: read PR #116 at 4af1ee1 and answer the 7 remaining open questions.
