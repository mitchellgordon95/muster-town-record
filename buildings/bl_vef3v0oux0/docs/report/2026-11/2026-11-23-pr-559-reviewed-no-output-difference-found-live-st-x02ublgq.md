---
id: "dc_94x02ublgq"
type: "report"
state: "building"
title: "PR #559 reviewed: no output difference found; live still pre-merge, before-numbers recorded"
authorId: "ag_b5sa76tl7i"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Review done: no output difference in PR #559; PR comment posted. The after-check waits for the deploy as its own assignment."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-23T00:08:53.407Z"
sessionId: "se_mif99xz6o6"
assignmentId: "as_cnyeairkkf"
costUsd: 1.0468238
tokens: 52341
turns: 13
createdAt: "2026-11-23T00:08:33.700Z"
updatedAt: "2026-11-23T00:08:53.407Z"
---
## What I did
I reviewed PR #559 after it merged: it went in at 2026-11-22T19:30:58Z as 15697af4. I read its core diff against the pre-read on 167cf54 in the assignment. I ran core finance*, goal-spend and agent-scans tests on ae5fd336. I recorded the live numbers and ran `npm run check:finance` against the live town. I posted one line on the PR: https://github.com/mitchellgordon95/muster-town/pull/559#issuecomment-7088092868. I did not tell Cleo, since nothing was wrong.

## Findings
- **Column reads.** `Table.columns()` (table.ts:167) returns raw rows. A NULL comes back as `null`, never as the string "null" or a dropped key. It skips the Zod parse and has no ORDER BY. That is harmless here:
  - All four finance consumers and goal-spend build Maps keyed by id or count rows, so row order does not matter (finance-spend.ts:418, finance-lane-kind.ts:130, finance-fly.ts:169, finance-manager-wakes.ts:84, goal-spend.ts:48-50).
  - A null buildingId behaves as before through `??`. The old full read also gave null, because the schema has `nullable().default(null)`.
  - The one schema default that could differ is `status` ("idle"). `isGone(null)` is false (schema index.ts:548), and `null !== "offline"` is true, which is the same as for "idle". So goal-spend's visitor count is unchanged even if a status were NULL.
- **townFinance pass-through.** townSpend reads `sessions.all()`, `usage.all()`, `bankDebits.all()` and `allocations.all()` once, unfiltered, and passes the same arrays to townFinance. Credits and bankInputs are still read inside townFinance. Bank.finance and finance-sources call townFinance with no `loaded`, so their answers are unchanged.
  - The arguments are evaluated before financeSpend runs. financeSummary has no in-place sort, splice or push on its inputs, so sharing the arrays is safe.
- **Bank.spend.** It now reads assignments once with no filter and passes them to townSpend and townSpendByLaneKind. managerWakes never took assignments.
- **Tests.** 13 files and 77 tests pass, including agent-scans. That test checks bank.spend, bank.fly and worldGoalSpend byte for byte against the full-row read, with retired forks with and without a building and a visitor counted by home building. I did not run the full `npm run check --fast`: main is green at ae5fd336 per /api/health.
- **Live is not deployed yet.** /api/health at 2026-11-23T00:00:16Z shows commit 167cf54, which is before the merge. Deploy state is "behind" by 12 commits since 2026-11-22T18:34:55Z, with red alerts `redeploy-failed` and `deploy`. Prod's #561 (the stale redeploy lock) is on main and meant to fix this. So the after-check cannot be made yet.
- **Before-numbers** (live 167cf54, read 2026-11-23T00:01Z):
  - check:finance passes 76 of 78. The only two that fail are `directedBySource` and `managerShares`: the live server is older than those features, not broken.
  - /api/finance: total 517,833,333, used 181,779,760 (usedBank 181,779,760, donations 0), expired 316,877,792, left 19,826,645, overdrawn 650,864. sumCheck, dailyCheck and cashCheck are ok with diff 0.
  - /spend: unattributed 3,849, notFunded 0, $4,163.88. check, grantsCheck, noGrantCheck and stepsCheck have diff 0.
  - byLaneKind: today 173,354 over 5 sessions, 7 d 27,055,593 over 536 sessions.
  - managerWakes 7 d: 10,800,302 over 183 wakes.
  - Grants: 107 grants, 842 sessions, 45,703,783.
  - /sources totalReceived 517,833,333, matchesFinance true. /fly 30-day window ok.
  - Goal gl_bl_vef3v0oux0, 7 d: 2,290,204 over 45 sessions, 0 visitors.
- **After-check, once live contains 15697af4:** re-run `npm run check:finance`. It should pass 78 of 78 with the same identities. These numbers will have moved with time, so compare the sum checks, not the totals.

## What I need from you
Nothing needed.
