---
id: "dc_0yo2agaodj"
type: "report"
state: "building"
title: "Bank Transparency: gr_gbpbbwy9b8 closed as done, funding sources live on the finance page (Total received 52,729,370 ✓, 12 inputs with dated credits + 4 donations); kr_j9058i256a claimed"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_u32mrdnzxn","dc_vwjbdmyrub","dc_egvxsz371o","dc_28e7o8wpga","dc_yunn9r2yxt"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T02:09:54.476Z"
sessionId: "se_qpmiixq8oo"
assignmentId: "as_wg0udxwzjc"
costUsd: 2.853697249999999
tokens: 57074
turns: 34
createdAt: "2026-10-29T00:51:07.653Z"
updatedAt: "2026-10-29T02:09:54.476Z"
---
Live at 5460f80 (checked 2026-10-29 00:47Z); cosmetic follow-up 090c169 on main, CI promoting.

## Shipped

**1. Sources section on the finance page (gr_gbpbbwy9b8, kr_j9058i256a)**
**What it is:** The finance page now shows where the town's tokens came from: every Bank input (subscription or API key) with its label, owner, first → last credit date and tokens, opening to its dated credits with expiry and expired-undrawn tokens; every direct donation with giver, building, date and tokens; subtotals and a Total received that is checked against the Tokens section's total. Backed by GET /api/finance/sources. Asha built both steps ([dc_u32mrdnzxn](2026-10-29-get-api-finance-sources-pushed-to-main-at-3c40a2a-2mrdnzxn.md), [dc_vwjbdmyrub](2026-10-29-sources-section-on-finance-pushed-to-main-at-5460f-jbdmyrub.md)); I verified live ([dc_egvxsz371o](2026-10-29-sources-step-1-reviewed-3c40a2a-reads-right-redepl-vxsz371o.md), [dc_28e7o8wpga](2026-10-29-sources-step-1-verified-live-at-3c40a2a-sumcheck-o-e7o8wpga.md)) and closed the grant: 241,493 / 300,000 spent, 58,507 returned to the Bank.
**What you'd see:** https://muster.town/workshop/#/finance, the Sources section above Spending. Live: 12 inputs (19 dated credits), 4 donations; Credited through the Bank 48,099,993 + Donated to buildings 4,629,377 = Total received 52,729,370, with "✓ Adds up … the Tokens section's total". API: sumCheck.ok true, totalReceived = /api/finance total, Σ expired credits 11,120,685 = Expired. /api/bank creditedTokens is 5 tokens higher (48,099,998: the running counter vs the per-credit sum), a rounding gap, not a missing source.
![Sources section on the finance page: donations, subtotals, Total received 52,729,370 ✓](/api/media/mf_i4c8fcywj2.png)
**Your call:** Mark kr_j9058i256a met or missed from this close report.

**2. Narrow-panel fix for Sources labels (090c169)**
**What it is:** At panel widths under ~350 px an input's label broke one letter per line beside its date range (flex basis 0 on the name column). One CSS line on main; web tests 109 green. I queued myself a live check once it deploys (as_v2adg8ct04).
**What you'd see:** Same page at a narrow window: labels read as words, the date range wraps after the arrow. Nothing changes in Spending. No picture (not live yet; CI is promoting it).
**Your call:** None.

## Decided
- [dc_yunn9r2yxt](2026-10-28-gr-gbpbbwy9b8-funding-sources-300k-cut-into-3-step-nn9r2yxt.md) → approve (grant cut into 3 steps)
- [dc_u32mrdnzxn](2026-10-29-get-api-finance-sources-pushed-to-main-at-3c40a2a-2mrdnzxn.md) → approve (step 1, GET /api/finance/sources at 3c40a2a)
- [dc_egvxsz371o](2026-10-29-sources-step-1-reviewed-3c40a2a-reads-right-redepl-vxsz371o.md) → approve (step 1 review, parked on deploy)
- [dc_28e7o8wpga](2026-10-29-sources-step-1-verified-live-at-3c40a2a-sumcheck-o-e7o8wpga.md) → approve (step 1 verified live, all sums match)
- [dc_vwjbdmyrub](2026-10-29-sources-section-on-finance-pushed-to-main-at-5460f-jbdmyrub.md) → approve (step 2, Sources section at 5460f80)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_j9058i256a funding sources | gr_gbpbbwy9b8 (closed as done) | claimed | 241,493 / 300,000 |
| kr_97kyvac8f4 pools and per-building allocation | none | not started | – |
| kr_mx4odqn5xt used / left / projected | gr_gi5jbgzv4k (closed) | met | – |
| kr_q9oiu7a6ci spend by building / grant / assignment | gr_8gtgmd828o (closed) | met | – |

Today's spend by lane: exploration 0 / 828,571 tokens, directed 0 tokens. No funded grant is open; kr_97kyvac8f4 needs a design call before a proposal (buildings have no allocation amount by design; the honest view is actual draws per building and the pools from /api/bank).

## Needs from Mitchell
Nothing needed.

_Nothing else waiting in your in-tray._
