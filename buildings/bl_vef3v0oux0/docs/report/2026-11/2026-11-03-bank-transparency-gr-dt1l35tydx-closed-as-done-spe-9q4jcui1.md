---
id: "dc_3t9q4jcui1"
type: "report"
state: "building"
title: "Bank Transparency: gr_dt1l35tydx closed as done, Spending tab grant lines live at 85498fa (close report)"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_tapqb5h610"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "pending"
sessionId: "se_vpkl3aqh8d"
createdAt: "2026-11-03T02:49:00.764Z"
updatedAt: "2026-11-03T02:49:00.764Z"
---
Live: 85498fa (since 02:47 UTC). This is the close report for gr_dt1l35tydx; the rollup filed a few minutes earlier ([dc_quybc4r5za](2026-11-03-bank-transparency-cost-estimate-step-2-live-overdr-ybc4r5za.md)) still covers #267 and the new goal.

## Shipped

**1. The Spending tab says what each grant bought (gr_dt1l35tydx closed as done)**
**What it is:** The Bank's Spending tab now opens with one sentence on grant spend by outcome (done / cut / still open, and how many grants ran over) plus a server-checked ✓ line, and every grant row under a building says what it spent against what it was funded, its outcome, how far over it is, and how many key results are met or claimed. PR #261 (merge dcfffe01), verified live at 85498fa2 by [dc_tapqb5h610](2026-11-03-spending-tab-grant-lines-verified-live-at-85498fa2-pqb5h610.md); `npm run check:finance` against live 32/32 ✓.
**What you'd see:** muster.town/workshop/?guest#/bank → Spending: "Grants: 18,880,630 tokens spent on 49 grants: 9,820,316 on 25 done, 2,593,904 on 6 cut, 6,466,410 on 18 still open. 12 grants spent more than they were funded (959,584 over in total)." then "✓ The server checked that spend on done, cut and still-open grants adds up to the grant rows". Expand Bank Transparency: e.g. "spent 401,636 of 300,000 funded · done · over by 101,636 · key results 0 of 4 met (4 claimed, waiting for a human)" (figures as read 02:47Z; they move as sessions run).
![Spending tab: opening sentence, ✓ line, a building row and two grant lines](/api/media/mf_r0e7vedcxc.png)
**Your call:** Mark kr_f5gx4nuzuu and kr_d3mh9gmk2k met or missed on the grant (Town Hall in-tray). 339,322 of 500,000 spent; 160,678 returned to the Bank.

## Decided
- [dc_tapqb5h610](2026-11-03-spending-tab-grant-lines-verified-live-at-85498fa2-pqb5h610.md) → approve (both KRs verified live; grant closed as done).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_dt1l35tydx (Spending tab, closed done) | kr_f5gx4nuzuu opening sentence + ✓ line | claimed | 339,322 / 500,000 |
| gr_dt1l35tydx | kr_d3mh9gmk2k one line per grant row | claimed | — |
| gr_4tf9hd64d5 (grant pages list sessions, funded) | KRs due 2026-11-09 | not started (step 1 as_76vjraki6o queued) | 0 / 200,000 |
| gr_gmzli3f96j (closed done 11-02) | kr_jksobb0bwo | claimed, awaiting your mark | 698,207 / 500,000 |

Spend today by lane: exploration 0 tokens (free under our goal 392,698), directed 119 tokens. Queue: as_76vjraki6o (grant step 1), as_ricjwkoaxc (verify the prompt-caching fix on first manager wakes).

## Needs from Mitchell
Nothing needed beyond the key-result marks on the grant card.

_Already waiting in your in-tray: 1 proposal (gr_lwgus14rd2), 0 requests, 2 rollups ([dc_4s6sdf5p6g](2026-11-02-bank-transparency-spending-tab-per-grant-lines-neg-6sdf5p6g.md), [dc_quybc4r5za](2026-11-03-bank-transparency-cost-estimate-step-2-live-overdr-ybc4r5za.md))._
