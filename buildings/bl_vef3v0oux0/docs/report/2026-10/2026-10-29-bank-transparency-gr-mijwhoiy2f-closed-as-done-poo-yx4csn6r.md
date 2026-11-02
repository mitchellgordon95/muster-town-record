---
id: "dc_ocyx4csn6r"
type: "report"
state: "building"
title: "Bank Transparency: gr_mijwhoiy2f closed as done, Pools section live on the finance page (General pool 100%, left 13,529,887, overdrawn −256,870; six buildings' draws Σ 31,008,859 = Bank debits, both ✓ lines); kr_97kyvac8f4 claimed, all four key results now met or claimed"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_vy63cph4hm","dc_a7s7yavb65","dc_4x5irqjesp"],"urls":["https://muster.town/workshop/?guest#/finance","https://muster.town/api/finance/pools","https://muster.town/api/health"]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T15:37:31.920Z"
sessionId: "se_z5w5z1jsgm"
assignmentId: "as_7u450se35s"
costUsd: 2.6067670499999993
tokens: 52135
turns: 23
createdAt: "2026-10-29T04:15:23.743Z"
updatedAt: "2026-10-29T15:37:31.920Z"
---
Live at e74ae79 (carries 0f1027b), checked 2026-10-29 04:12Z.

## Shipped

**1. Pools and per-building draws on the finance page**
**What it is:** The last of the four Bank Transparency key results. A new public endpoint GET /api/finance/pools (Asha, step 1, 168d8bb, [dc_vy63cph4hm](2026-10-29-get-api-finance-pools-on-main-at-168d8bb-pools-pct-63cph4hm.md)) and a Pools section on the finance page between Sources and Spending (Asha, step 2, 0f1027b, [dc_a7s7yavb65](2026-10-29-pools-section-on-finance-pushed-to-main-at-0f1027b-s7yavb65.md)). Each pool shows its share, tokens left (expiring and permanent), all-time draws and, when it applies, a red "overdrawn" line for permanent tokens drawn past its share. Under it, each building shows what it drew from its pool, its donations, what of them it still holds, and its daily exploration allowance. Two check lines prove the numbers add up. Step 3 (me, [dc_4x5irqjesp](2026-10-29-pools-step-3-parked-on-deploy-0f1027b-live-api-at-5irqjesp.md) and this report) verified it live at 1000 and 1400 px and closed the grant: gr_mijwhoiy2f done at 200,677 of 300,000 tokens, 99,323 returned to the Bank; kr_97kyvac8f4 claimed.
**What you'd see:** muster.town, the "$" HUD button, `#/finance`, fourth section "Pools". On 2026-10-29 04:12Z: General · all 6 buildings, 100%, left 13,529,887 (expiring 13,529,887 · permanent 0 · drawn all time 31,008,859); "General overdrawn: permanent tokens drawn past its share −256,870"; "Bank balance less overshoot 13,273,017"; "✓ Adds up: pools left 13,529,887 − overdrawn 256,870 = 13,273,017; Bank balance 13,529,887 − overshoot 256,870 = 13,273,017". Then Town Hall 0 (draws nothing from the Bank), Town Workshop 17,208,720 (donated 4,629,377), Onboarding 6,008,883, Prod 3,454,645, Bank Transparency 2,257,988, Code Legibility and Maintenance 2,078,623; "Drawn from pools 31,008,859"; "✓ Adds up: building draws = pool draws = Bank debits = 31,008,859". Numbers move daily (a 15,000,000 credit lands each day).
![Pools section at 1400 px: General pool with overdrawn line and its ✓ (left), per-building draws with their ✓ (right)](/api/media/mf_rfjqa2xpms.png)
**Your call:** Mark kr_97kyvac8f4 met or missed. The page shows what each building actually drew, not a planned allocation, because buildings have none in the Bank (first come, first served inside a pool); if you want planned per-building allocations, that is a schema and Bank change for a new key result.

## Decided
- [dc_vy63cph4hm](2026-10-29-get-api-finance-pools-on-main-at-168d8bb-pools-pct-63cph4hm.md) (Asha, step 1: GET /api/finance/pools, 168d8bb) → approve.
- [dc_a7s7yavb65](2026-10-29-pools-section-on-finance-pushed-to-main-at-0f1027b-s7yavb65.md) (Asha, step 2: Pools section, 0f1027b, 117/117 web tests) → approve.
- [dc_4x5irqjesp](2026-10-29-pools-step-3-parked-on-deploy-0f1027b-live-api-at-5irqjesp.md) (Nell, step 3 parked on the deploy; resumed and finished in this report) → approve.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_97kyvac8f4 pools and per-building allocation | gr_mijwhoiy2f (closed as done 04:13Z) | claimed | 200,677 / 300,000 (99,323 returned) |
| kr_mx4odqn5xt, kr_q9oiu7a6ci, kr_j9058i256a | gr_gi5jbgzv4k, gr_8gtgmd828o, gr_gbpbbwy9b8 (closed) | met | — |

No funded grant remains. Today's spend by lane: exploration 84,535 / 828,571 tokens, directed 146,878 tokens.

## Needs from Mitchell
Nothing needed beyond the call above. With all four key results met or claimed, the building goal has no open key result; new Bank Transparency work needs a key result from you (a 1:1 or a note) before I propose a grant.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_jx27xnwz2d](../../../../../town-hall/outbox/2026-10/2026-10-29-bank-transparency-forks-step-1-done-flip-budget-mo-27xnwz2d.md)), 0 rollups._
