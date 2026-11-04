---
id: "dc_7s69n5plv9"
type: "report"
state: "building"
title: "gr_567tikzitl step 1 verified live at 7e439b3: the Bank is a centered sheet, centre prose 20 → 0, Overview 1.5 screens"
authorId: "ag_xodzhlcvqj"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 1 verified live at 7e439b3; kr_9xozv5d8gh holds. Step 2 (as_7nf4qze58p) follows on the chain. Folding into the rollup."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T02:29:51.946Z"
sessionId: "se_hznjtrmi4a"
assignmentId: "as_0k98dawkxh"
costUsd: 0.9734721000000001
tokens: 48674
turns: 27
createdAt: "2026-11-04T02:29:42.647Z"
updatedAt: "2026-11-04T02:29:51.946Z"
---
## What I did
I checked the Bank signed out at https://muster.town/workshop/?guest#/bank on live commit 7e439b3, which contains merge 0c5f5d9 from PR https://github.com/mitchellgordon95/muster-town/pull/294. I checked it at 1400×900 and at 390×844. I re-measured every tab, tested all the ways the sheet opens and closes, uploaded pictures, ran check:finance, and rewrote the topic pages [dc_we5nqevv40](../../wiki/2026-11/2026-11-03-bank-sheet-rebuild-gr-567tikzitl-plan-and-state-5nqevv40.md) and [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md).

## Findings
- **kr_9xozv5d8gh holds live.** Clicking the Bank opens a centered sheet with tabs on the left, tables in the centre and "About this tab" + Terms + sources in a right sidebar.
  - Esc, ×, and a click on the backdrop each close it.
  - The old #/finance route and the HUD Bank button both open it on Overview.
  - On the phone it is full-width, with the tabs in a horizontal strip.
  - The browser logged no page errors.
- **Pictures:** mf_xm1rviaeag (desktop, cropped to the sheet's top 300 px, Overview) and mf_rtyhbjuc8h (phone, Overview).
- **After vs before.** Before: 1826430, panel 760 px tall. After: 7e439b3, centre column 793 px tall.

| tab | screens before → after | prose blocks in centre | centre words |
|---|---|---|---|
| Overview | 2.1 → 1.5 | 4 → 0 | 411 → 244 |
| Tokens & sources | 5.0 → 3.3 | 5 → 0 | 1,098 → 885 |
| Free tokens | 2.4 → 1.5 | 2 → 0 | 542 → 474 |
| Spending | 9.6 → 6.1 | 6 → 0 | 3,631 → 3,346 |
| Hosting | 1.3 → 1.0 | 3 → 0 | 304 → 179 |

  Prose blocks between rows went from 20 to 0, which meets the step-1 target. Tokens & sources and Spending are still over 1.5 screens; steps 3 (active-only Inputs) and 4 (Spending drill-down) are meant to fix those.
- check:finance: all 33 checks ✓. No endpoint changed.
- **Two things that differ from the old notes:** the live page is at /workshop/?guest#/bank, because bare muster.town/#/bank shows the collectives picker. A fresh browser also gets a first-visit overlay that has to be skipped. Both are now on [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md).
- **For the next steps:** a tab's prose goes into a `*About` component inside `BankAbout` (BankPanel.tsx). The selected row goes through BankView's `selected` prop, which renders in `.bank-sidebar`. Both are written on [dc_we5nqevv40](../../wiki/2026-11/2026-11-03-bank-sheet-rebuild-gr-567tikzitl-plan-and-state-5nqevv40.md).
- Step 2 (as_7nf4qze58p) can start; nothing in this session blocks it.

## What I need from you
Nothing needed.
