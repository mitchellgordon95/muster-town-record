---
id: "dc_4rb4ipqjz6"
type: "report"
state: "building"
title: "Rollup 55: \"From first visit to owning a goal\" closed as done: the test account captained a goal, steered it live, and reset itself; 388,193 tokens back to the Bank"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_jklevfwy28","dc_iwpdkuduif"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "pending"
sessionId: "se_pug9wpajlp"
createdAt: "2026-11-10T17:22:22.866Z"
updatedAt: "2026-11-10T17:22:22.866Z"
---
Live e0ce780 since 00:27 UTC today (nothing new deployed since rollup 54; this rollup closes a grant).

## Shipped

**1. A member can ask to captain a goal, be accepted, and steer it: proven end to end, grant closed**

**What it is:** The whole road you funded on Oct 31 now holds in the live town. The test account (a plain member) asked to captain the Join goal, you accepted it from the in-tray on Nov 6, and today, signed in as that captain, its Town Hall in-tray opened on Mine with Outreach's proposal under that goal routed to it with Fund, Counter and Reject in hand. Nothing was clicked on the proposal. The account then ran the first live reset of itself: back to visitor only, the goal's captain cleared, so it inherits you again. Tests for member-only asks, routing to the current captain, accept sets the captain and decline leaves it unset are on main. On that evidence I closed the grant as done one minute after your adjust: gr_bwm0iz7rwl, 511,807 of 900,000 spent, 388,193 returned to the Bank, all four key results met ([dc_jklevfwy28](2026-11-10-test-account-steered-its-goal-gr-uc179zv1xa-routed-levfwy28.md), [dc_fazgj1xueq](2026-11-06-publish-to-github-re-check-still-no-repo-set-anywh-zgj1xueq.md), [dc_hie8bsm5ch](../2026-10/2026-10-31-ask-to-captain-a-goal-192-a10095d-is-live-and-chec-e8bsm5ch.md), PR #192).

**What you'd see:** Goal tree: the Join goal (ob_508f35a2m4) shows no captain again. Town Hall in-tray: Outreach's proposal gr_uc179zv1xa is routed back to you. The grant row for "From first visit to owning a goal" reads closed, done, with four key results met. This session's check was API-only (GET /api/me and the in-tray as the account), so no new picture; the earlier crops are on the grant's reports.

**Your call:** None. If one of the four key results does not hold for you, flip it to missed from the grant.

## Decided
- [dc_jklevfwy28](2026-11-10-test-account-steered-its-goal-gr-uc179zv1xa-routed-levfwy28.md) → approve (steer check passed, first live reset clean; grant closed on it)
- [dc_iwpdkuduif](2026-11-10-grant-gr-bwm0iz7rwl-adjusted-900-000-tokens-pdkuduif.md) → approve (your adjust to 900,000 released the held step by itself; its report is the one above)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_bwm0iz7rwl From first visit to owning a goal (closed, done) | kr_j1w17nw178 member asks to captain, captain accepts, new captain sees Mine with Fund/Counter/Reject | met | 511,807 / 900,000 |
| gr_bwm0iz7rwl | kr_07d30db2bf core and server tests | met | |
| gr_bwm0iz7rwl | kr_fd3ac479eb the request shows where a decider looks | met | |
| gr_bwm0iz7rwl | kr_917dc5ba6d the new captain steers their subtree live | met | |
| gr_mjr7nb438v Keep onboarding material within 24 h of main | kr_hee2pa2d5r | on-track, no session today | unchanged since rollup 54 |
| gr_30f8obzab8 Any collective publishes its docs to GitHub | its key results | no session today | unchanged since rollup 54 |

Spend today by lane: grant 50,336 (gr_bwm0iz7rwl step 3b), exploration 132,078, directed 0. Free under the Join goal: 13,211,646 before the close; the 388,193 returned adds to it.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_8bxoy2heif), 0 requests, 3 rollups ([dc_430cifl3v5](2026-11-06-rollup-50-grants-a-b-c-and-the-throwaway-closed-1-0cifl3v5.md), [dc_hf4ziawngu](2026-11-06-rollup-51-the-stranger-test-account-is-in-asked-to-4ziawngu.md), [dc_y3pqu4tfip](2026-11-07-rollup-52-onboarding-sweep-10-live-manual-fixed-th-pqu4tfip.md))._
