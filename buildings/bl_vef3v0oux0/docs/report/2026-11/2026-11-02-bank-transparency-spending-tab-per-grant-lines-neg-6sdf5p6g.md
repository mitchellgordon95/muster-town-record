---
id: "dc_4s6sdf5p6g"
type: "report"
state: "building"
title: "Bank Transparency: Spending tab per-grant lines, negative FREE sign and history-based grant cost ranges are live; grant steps held by the overdraft"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_v836ng1nv4","dc_ohxd9xzfy0","dc_22qkds5f4n","dc_sa2lpxvmut","dc_5iwfy2q1or","dc_a904semn8e","dc_oymdhq3pz6","dc_oke31fn1e3"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/261","https://github.com/mitchellgordon95/muster-town/pull/262","https://github.com/mitchellgordon95/muster-town/pull/263"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_8e5khf4lem"
createdAt: "2026-11-02T18:04:53.086Z"
updatedAt: "2026-11-02T18:04:53.086Z"
---
Live: 92336d0e since 18:02 UTC today. It carries three of ours that sat merged on main for about 14 hours without a deploy (main's CI runs were cancelled by later pushes; Nell 2 queued the redeploy at 18:00 UTC).

## Shipped

**1. The Spending tab says what each grant bought**
**What it is:** Step 1 of the funded grant gr_dt1l35tydx (PR #261, merged dcfffe01). Every grant row on the Bank's Spending tab reads spent vs funded with its outcome (done / cut / open) and its key results, and the tab opens with one sentence totalling grant spend by outcome and how many grants spent more than they were funded. Outcome mapping: done or met → done; cut, stopped, spent or rejected → cut; everything else open.
**What you'd see:** Signed out, muster.town/#/bank → Spending. The opening sentence read, on the data at 03:09 UTC today, about 17.35M adj. tokens spent on 44 grants (25 done, 9.82M; 6 cut, 2.59M; 13 open, 4.94M), 13 over funding by 1.14M in total. Expand a building: each grant row carries its own "spent X of Y funded · outcome · over by Z" line. No picture yet: the live check with a cropped picture is step 2 (as_8mbeonpgic), which is held (see Needs).
**Your call:** None.

**2. The Bank sign shows FREE as freeTokens minus overdraft, red when negative**
**What it is:** Your flag [dc_jlqnc3d36r](../../flag/2026-11/2026-11-02-i-think-we-can-show-overdraft-as-negative-free-tok-qnc3d36r.md), PR #262 (merged 2b8ba6e). The Bank marquee's FREE column now subtracts the overdraft and turns red below zero instead of showing a free figure the town can't spend.
**What you'd see:** Signed out, muster.town/#/bank: the FREE figure in the marquee is negative and red. At 03:20 UTC it would have read about −712,236; the overdraft figure later read 3,281,745 on /api/finance, so the live number is larger. A directed fork (as_kfhwg4x4fh) is about to verify the live value, take the picture and explain that jump; its report goes in the next rollup.
**Your call:** None.

**3. Every grant proposal shows what similar closed grants spent, beside the ask**
**What it is:** Step 1 of your 1:1 ask (mt_c9u1kr15jp) for a history-based grant cost estimate, PR #263 (merged 177e292e). No model involved: the range comes from closed grants' actual spend. API-only plus the proposal line: `propose_grant` now answers with an `estimate` line, and the grant page shows the range.
**What you'd see:** On the grant page of gr_4tf9hd64d5 the range reads 176,158–238,987 adj. tokens against its 200,000 ask; on gr_dt1l35tydx 176,158–289,904 against 500,000. Step 2 (a cheap-model estimate shown beside the ask and compared with the actual at close, PR #267) is merging now (Nell 1, as_e17ejwrohu) and will be in the next rollup with its per-call cost.
**Your call:** None.

## Decided
- [dc_v836ng1nv4](2026-11-02-pr-261-was-already-merged-dcfffe01-but-never-went-36ng1nv4.md) (Nell 2: #261 was already merged, redeploy queued) → approve.
- [dc_ohxd9xzfy0](2026-11-02-grant-cost-estimate-step-2-pr-267-built-and-tested-xd9xzfy0.md) (Nell 1: cost estimate step 2, PR #267 built, #261 merged) → approve; continuation as_e17ejwrohu running.
- [dc_22qkds5f4n](2026-11-02-pr-263-grant-cost-estimate-step-1-merged-as-177e29-qkds5f4n.md) (Nell 2: #263 merged 177e292e) → approve.
- [dc_sa2lpxvmut](2026-11-02-pr-262-merged-2b8ba6e-redeploy-queued-live-sign-no-2lpxvmut.md) (Nell 1: #262 merged 2b8ba6e) → redirect to as_kfhwg4x4fh (verify live, picture, explain the overdraft jump).
- [dc_5iwfy2q1or](2026-11-02-pr-262-had-a-merge-conflict-with-main-resolved-par-wfy2q1or.md) (Nell 1: #262 conflict resolved) → approve.
- [dc_a904semn8e](2026-11-02-grant-cost-estimate-step-1-pr-263-built-and-tested-04semn8e.md) (Nell 1: #263 built) → approve.
- [dc_oymdhq3pz6](2026-11-02-bank-sign-negative-free-tokens-pr-262-open-parked-mdhq3pz6.md) (Nell 2: #262 open) → approve.
- [dc_oke31fn1e3](2026-11-02-exploration-grant-pages-don-t-list-their-sessions-e31fn1e3.md) (Nell 1: exploration, proposed gr_4tf9hd64d5) → approve; you funded it, step 1 queued as as_76vjraki6o.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_dt1l35tydx Spending tab | kr_d3mh9gmk2k every grant row reads spent vs funded + outcome + KRs | not-started (code live, signed-out check pending in step 2, held) | 283,366 / 500,000 |
| gr_dt1l35tydx | kr_f5gx4nuzuu opening sentence totals spend by outcome | not-started (same) | 283,366 / 500,000 |
| gr_4tf9hd64d5 grant page sessions | kr_tqjylvupko grant page lists its sessions, footer = spent | not-started (step 1 queued 18:08 UTC, as_76vjraki6o) | 0 / 200,000 |
| gr_4tf9hd64d5 | kr_o550w4u25b GET /api/sessions?grantId + check:finance line | not-started (same) | 0 / 200,000 |

Today's spend by lane: exploration 48,270 tokens (free under our goal: 0), directed 464,195 tokens.

## Needs from Mitchell
1. The Bank is overdrawn, so funded-grant steps are held: the queue shows as_8mbeonpgic (gr_dt1l35tydx step 2) "held: overdrafted, the Bank's usable balance doesn't cover", since about 14 hours ago, and the new gr_4tf9hd64d5 step 1 will likely be held the same way. Add tokens to the Bank (or say which of the two grants should go first) so the funding you gave can run; nothing else unblocks them.
2. Mark the dollars grant's last key result kr_jksobb0bwo met or missed: the Bank reads in dollars at API list price signed out (the check is in that grant's close report from 02:05 UTC today).

_Nothing else waiting in your in-tray._
