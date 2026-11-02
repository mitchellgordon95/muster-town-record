---
id: "dc_9if1je62bo"
type: "report"
state: "building"
title: "gr_glon8xr0io closed as done: the `open` budget mode is gone from main (PR #70 merged at 9890055, CI green attempt 1); kr_ef11f6ex28 claimed"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vnvhyuagpo","dc_nfdgkryb3s","dc_32p3strium"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/70"]}
tags: ["rollup","grant-close","parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T23:17:45.104Z"
sessionId: "se_42totg6tro"
assignmentId: "as_qavhj20x1y"
costUsd: 1.5821714000000002
tokens: 31643
turns: 18
createdAt: "2026-10-28T20:54:25.361Z"
updatedAt: "2026-10-28T23:17:45.104Z"
---
Live is 222e229; 9890055 should be live after the redeploy that is waiting on this session (town.redeploy refuses us; Nell told the commit as fallback).

## Shipped
**1. The `open` budget mode is gone: every lab is goal-directed, the Town Hall never is**
**What it is:** The last building flag from your town-hall decision 3. The lane gate, grants, prompts, the board's key-results block and the REST routes now decide by building kind instead of a stored mode; `budgetMode` survives only as a schema column (so old rows parse) and nothing reads it. Core + schema + 17 test files (Finn, [dc_vnvhyuagpo](2026-10-28-remove-open-budget-mode-step-1-draft-pr-70-d2ea086-vhyuagpo.md)), web + 7 docs + forks tests fixed at the root (Finn, [dc_nfdgkryb3s](2026-10-28-remove-open-budget-mode-step-2-pr-70-ready-head-73-dgkryb3s.md)), review and merge by me. PR #70 merged at 9890055; main CI run 40766932867 green on attempt 1. Regression test `lanes.test.ts` "every lab is lane-gated, even one created without budgetMode or with a stale open row; the Town Hall never is", cited by invariant 1 of docs/invariants/assignments-lanes.md. Grant gr_glon8xr0io closed as done: 207,344 of 250,000 tokens spent, 42,656 returned to the Bank.
**What you'd see:** Once 9890055 is live (GET /api/health shows `commit`): any Building → Settings on muster.town has no "Budget mode" select, only Exploration / day and Forks; the Town Hall board shows no key-results block; GET /api/health `budgets` lists the five labs and not the Town Hall; a lab manager's `assign` without a lane is refused. No picture: the change is not live until this session ends, so there is nothing new to crop yet.
**Your call:** Mark kr_ef11f6ex28 met (or missed) in the Town Hall in-tray.

## Decided
- [dc_vnvhyuagpo](2026-10-28-remove-open-budget-mode-step-1-draft-pr-70-d2ea086-vhyuagpo.md) (Finn, step 1: core + schema + tests, draft PR #70) → approve.
- [dc_nfdgkryb3s](2026-10-28-remove-open-budget-mode-step-2-pr-70-ready-head-73-dgkryb3s.md) (Finn, step 2: web + docs, PR ready, CI green attempt 1, forks tests fixed at the root) → approve.
- [dc_32p3strium](2026-10-28-gr-glon8xr0io-remove-open-budget-mode-cut-into-3-s-p3strium.md) (Mara, the grant cut into 3 steps) → approve.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_ef11f6ex28 dead code (flags explicit) | gr_glon8xr0io, closed as done 21:10Z | claimed | 207,344 / 250,000 |

No funded grant is open now. Proposals awaiting you in the in-tray: gr_8ve21typt6 (abstraction consolidation, 260k), gr_x5gnnmo7yi (keep main green on attempt 1, 150k). Today's spend by lane: exploration 353,627 / 828,571 tokens, directed 47,607 tokens.

## Needs from Mitchell
Nothing needed. (The KR met/missed mark is in the in-tray, so it is not listed here.)
