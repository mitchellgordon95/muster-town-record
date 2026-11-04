---
id: "dc_d1tq1p4kgj"
type: "report"
state: "building"
title: "Bank Transparency: gr_567tikzitl closed done (845k of 1.5M spent); Bank opens on Donate, Inputs shows active rows only, Spending is a drill-down of about one screen per level"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_2iyvieytqu","dc_qaep9kkfvk","dc_d6ypu66efr","dc_stkfztyka9","dc_jo1kkik5ik"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:39.045Z"
sessionId: "se_liivkqnc23"
createdAt: "2026-11-04T04:04:13.967Z"
updatedAt: "2026-11-04T17:59:39.045Z"
---
Live: a84ed22 (PR #299, since 04:01 UTC). This rollup closes gr_567tikzitl: all five key results met, 845,383 of 1,500,000 tokens spent, 654,617 returned to the Bank.

## Shipped

**1. The Bank opens on Donate, and the chest in the Bank room opens it too**
**What it is:** The first tab a visitor sees is Donate (the funding form), not Overview; walking a guest into the Bank room and clicking the chest opens the same tab; the fountain is gone. Balance gained a "Free for exploration N" line so the number the town spends freely is on the page. PR #296 → a092a79; kr_00lym2zmif, kr_lq1qmywinq; verified signed out in [dc_stkfztyka9](2026-11-04-gr-567tikzitl-step-2-verified-live-at-a092a79-bank-kfztyka9.md).
**What you'd see:** https://muster.town/workshop/?guest#/bank lands on Donate; Balance shows "Free for exploration 508,936" (the figure at this session's start).
![Bank opens on Donate](/api/media/mf_f5a02xnh7z)
**Your call:** None.

**2. Inputs shows only active inputs; a clicked input's credits show in the sidebar**
**What it is:** The Inputs tab lists the 3 active inputs and folds the 15 cancelled ones behind "Show 15 cancelled". Clicking an input puts its credits in the right sidebar instead of a second table. The tab went from 3.3 screens to 1.33 at 1400×900. PR #298 → 664a0ea; kr_y7derda40x; verified in [dc_d6ypu66efr](2026-11-04-gr-567tikzitl-step-3-verified-live-at-664a0ea-inpu-ypu66efr.md) (pictures mf_4pgyqgqjo5, mf_7l5lhzkits, mf_ebcslh9fag).
**What you'd see:** Bank › Inputs: three rows and a "Show 15 cancelled" button; click a row and the sidebar reads its credits.
**Your call:** None.

**3. Spending is a drill-down: buildings › grants › assignments, one table per level**
**What it is:** The Spending tab was one 6.1-screen table. It is now one level at a time with a breadcrumb ("All buildings › Town Workshop › …"); the clicked row's detail (spent, share, its sessions) is in the sidebar. Measured at 1400×900: buildings 1.00 screen (10 rows), Town Workshop's grants 1.12 (11 rows), the biggest grant's assignments 1.86 (19 rows; long titles wrap). PR #299 → a84ed22; kr_trhi5frg4k; verified in [dc_2iyvieytqu](2026-11-04-gr-567tikzitl-step-4-verified-live-at-a84ed22-spen-yvieytqu.md). The "By goal" toggle still swaps in the existing spend-by-goal table (BankSpending.tsx:59); it was not photographed this pass.
**What you'd see:** Bank › Spending: used 105,509,773 adj. tokens (≈ $2,805.39), Town Workshop 59,263,965 (56.2%); click a building, then a grant; the breadcrumb goes back. Grants: 24,226,439 spent across 51 (34 done, 6 cut, 11 open; 10 over their funding by 757,640 in total). check:finance 33/33.
![Spending level 3 with the selected assignment in the sidebar](/api/media/mf_xvw7x7a0oz)
**Your call:** None.

## Decided
- [dc_jo1kkik5ik](2026-11-04-gr-567tikzitl-step-2-pr-296-merged-as-a092a79-rede-1kkik5ik.md) → approve (step 2 merged as a092a79, redeploy queued)
- [dc_stkfztyka9](2026-11-04-gr-567tikzitl-step-2-verified-live-at-a092a79-bank-kfztyka9.md) → approve (step 2 verified live)
- [dc_d6ypu66efr](2026-11-04-gr-567tikzitl-step-3-verified-live-at-664a0ea-inpu-ypu66efr.md) → approve (step 3 verified live at 664a0ea)
- [dc_qaep9kkfvk](2026-11-04-gr-567tikzitl-step-4-pr-299-merged-as-a84ed22-rede-ep9kkfvk.md) → approve (step 4 merged as a84ed22, redeploy queued)
- [dc_2iyvieytqu](2026-11-04-gr-567tikzitl-step-4-verified-live-at-a84ed22-spen-yvieytqu.md) → approve (step 4 verified live); then close_grant gr_567tikzitl as done

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_567tikzitl (closed done) | kr_9xozv5d8gh Bank is a centered sheet | met | 845,383 / 1,500,000 |
| gr_567tikzitl | kr_00lym2zmif opens on Donate, chest opens it | met | " |
| gr_567tikzitl | kr_lq1qmywinq Balance "Free for exploration" line | met | " |
| gr_567tikzitl | kr_y7derda40x Inputs active-only + selected input | met | " |
| gr_567tikzitl | kr_trhi5frg4k Spending drill-down | met | " |

No funded grant is open in this building now. Spend today by lane: exploration 0, directed 0 (free under the goal at session start: 508,936; the close returned 654,617 more).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_lwgus14rd2), 0 requests, 1 rollup ([dc_q3eagca1rb](2026-11-04-bank-transparency-gr-567tikzitl-step-1-live-the-ba-eagca1rb.md))._
