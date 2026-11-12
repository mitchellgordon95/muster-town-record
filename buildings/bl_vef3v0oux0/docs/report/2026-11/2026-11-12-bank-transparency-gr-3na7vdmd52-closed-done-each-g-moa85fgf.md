---
id: "dc_jbmoa85fgf"
type: "report"
state: "building"
title: "Bank Transparency: gr_3na7vdmd52 closed done, each grant step now shows its price and spend on the Bank page"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_j2lp0ewf84","dc_q929v42ido","dc_929tcfjgy1","dc_bahcaxv7lo","dc_7dcad9br4a"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "pending"
sessionId: "se_g9i0oabohh"
createdAt: "2026-11-12T16:08:15.707Z"
updatedAt: "2026-11-12T16:08:15.707Z"
---
Live: 7c182fe7 since 16:02 UTC today; it contains PR #431 (847b30af), the whole of this grant.

## Shipped
**1. Each grant step shows its price and spend on the Bank page**
**What it is:** On Bank › Spending, every grant funded with sized steps now opens into one row per step: its size, its price, what it spent, the ratio, and whether it is done or running, plus an Off-step row for sessions outside a step. The rows add up to the grant row on all 11 step-priced grants, and a ✓ line says so. The sidebar carries a calibration line: the median spent ÷ price per size over steps done in the last 30 days. Each step box's tooltip gives the same figures and a step past 1.5× its price gets a red border. check:finance 54 of 54 pass. Grant gr_3na7vdmd52, report [dc_j2lp0ewf84](2026-11-12-step-rows-calibration-line-and-step-tooltips-are-l-lp0ewf84.md).
**What you'd see:** https://muster.town/workshop/?guest#/bank › Spending, signed out. Code Legibility › "Bring the CI check back under 3 minutes" opens into "Step 1 · M step · price 150,000 · spent 70,032 · 0.47× its price · done" and so on; the rows total 175,650, the same as the grant row. The sidebar reads "S (price 50,000) 1.63× over 1 step · M (price 150,000) 0.95× over 10 steps · L (price 400,000) 0.77× over 1 step". GET /api/finance/spend: 14 step rows and 4 Off-step rows, 2,333,643 adjusted tokens, stepsCheck ok with diff 0.
![Step rows under a grant on Bank › Spending](/api/media/mf_o3vtkobyvf)
![A step box's tooltip with spent, price and ratio](/api/media/mf_25608vwj4q)
**Your call:** None. You adjusted this grant to 300,000 at 16:03 UTC today; it closed done at 247,796 spent and 52,204 returned to the Bank. Caveats: the calibration counts only steps done in the last 30 days, so S and L rest on 1 step each; grants funded before step sizes existed show no step rows.

## Decided
- [dc_7dcad9br4a](2026-11-12-step-rows-step-calibration-line-and-step-spend-on-cad9br4a.md) → approve (step 1: PR #431 opened, parked on CI)
- [dc_bahcaxv7lo](2026-11-12-pr-431-merged-as-847b30af-waiting-for-it-to-go-liv-hcaxv7lo.md) → approve (PR #431 merged as 847b30af, parked on deploy)
- [dc_929tcfjgy1](2026-11-12-grant-gr-3na7vdmd52-adjusted-300-000-tokens-9tcfjgy1.md) → approve (hold at 200,000 released by your adjust to 300,000)
- [dc_j2lp0ewf84](2026-11-12-step-rows-calibration-line-and-step-tooltips-are-l-lp0ewf84.md) → approve (live verification signed out, both key results claimed; grant closed done)
- [dc_q929v42ido](2026-11-12-duplicate-of-nell-1-s-verification-grant-already-c-29v42ido.md) → approve (duplicate verify fork stopped early)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_3na7vdmd52 Each grant step shows its price and spend | kr_jap500c8u3 step rows add up to grant rows on every step-priced grant | met (closed done) | 247,796 / 300,000 |
| gr_3na7vdmd52 | kr_5j25451emh calibration line per size on the Bank page | met (closed done) | 247,796 / 300,000 |

No funded grant remains. Spend today by lane: grant 247,796 (whole grant, 204,403 of it before today's last session), exploration 0, directed 0. Exploration stays paused at your ask of 11-10.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 1 rollup ([dc_3qryklj0hu](2026-11-10-bank-transparency-gr-utygatbi85-closed-done-the-no-ryklj0hu.md))._
