---
id: "dc_q3eagca1rb"
type: "report"
state: "building"
title: "Bank Transparency: gr_567tikzitl step 1 live, the Bank is a centered sheet (prose between rows 20 → 0, Overview 1.5 screens); step 2 (Donate first + chest) running"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_7s69n5plv9"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/294","https://muster.town/workshop/?guest#/bank"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:39.037Z"
sessionId: "se_hlb67gdt6p"
createdAt: "2026-11-04T02:30:52.009Z"
updatedAt: "2026-11-04T17:59:39.037Z"
---
Live: 7e439b3 (contains our merge 0c5f5d9 = PR #294, live since the 02:23Z redeploy).

## Shipped

**1. The Bank opens as a centered sheet: tabs left, one table in the centre, explanations in a right sidebar**
**What it is:** Step 1 of the funded Bank UX pass gr_567tikzitl (kr_9xozv5d8gh), PR #294 merged as 0c5f5d9. The side panel is gone; the Bank is a centered sheet over the map like the goal editor. Every explanatory paragraph moved from between table rows into a right sidebar ("About this tab", Terms, sources). Esc, × and a backdrop click close it; the old #/finance route and the HUD Bank button open it on Overview; on a phone it is full-width with the tabs in a horizontal strip. No endpoint changed (check:finance 33/33). Verified signed out at 1400×900 and 390×844 ([dc_7s69n5plv9](2026-11-04-gr-567tikzitl-step-1-verified-live-at-7e439b3-the-69n5plv9.md)).
**What you'd see:** Click the Bank on the map (or `/workshop/?guest#/bank`): a centered sheet. Prose blocks between rows: 20 → 0 across the five tabs. Screens to scroll: Overview 2.1 → 1.5, Tokens & sources 5.0 → 3.3, Free tokens 2.4 → 1.5, Spending 9.6 → 6.1, Hosting 1.3 → 1.0. Tokens & sources and Spending are still over 1.5 screens; steps 3 (active-only lists) and 4 (Spending drill-down) are the ones meant to fix that.
![The Bank as a centered sheet, Overview tab, desktop](/api/media/mf_xm1rviaeag)
**Your call:** None (step 2, Donate first with a chest in the Bank room and the fountain gone, is already running on Nell 2 as as_7nf4qze58p).

## Decided
- [dc_7s69n5plv9](2026-11-04-gr-567tikzitl-step-1-verified-live-at-7e439b3-the-69n5plv9.md) → approve (step 1 verified live at 7e439b3; kr_9xozv5d8gh holds; step 2 follows on the chain).

## Key results
gr_567tikzitl funded 1,500,000; step-1 sessions I have figures for: build 151,178 + merge 14,121 adjusted tokens (the verify session's figure is on the grant page; I could not read it from here).

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_567tikzitl (funded) | kr_9xozv5d8gh Bank as a centered sheet, prose in the sidebar | shipped and verified live (claim at close) | ≥165,299 / 1,500,000 |
| gr_567tikzitl (funded) | kr_00lym2zmif Donate first tab + chest fixture | in progress (as_7nf4qze58p, started 02:30Z) | — |
| gr_567tikzitl (funded) | kr_lq1qmywinq Free tokens tab and fountain gone, Balance shows "Free for exploration: N" | in progress (as_7nf4qze58p) | — |
| gr_567tikzitl (funded) | kr_y7derda40x active-only lists, row history in sidebar | not started (step 3, queued after step 2's report) | — |
| gr_567tikzitl (funded) | kr_trhi5frg4k Spending drill-down | not started (step 4, queued after step 2's report) | — |
| gr_lwgus14rd2 (proposed) | kr_pzr1fkgas8, kr_f49co6lg51, kr_avafh64h02 token cost legible and watched | awaiting funding decision | 0 / 600,000 ask |

Spend today by lane: exploration 0 tokens (free under our goal: 0), directed 0 tokens; all of today's work is on grant gr_567tikzitl.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_lwgus14rd2), 0 requests, 0 rollups._
