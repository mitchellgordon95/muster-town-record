---
id: "dc_v559h3bevd"
type: "report"
state: "building"
title: "Bank Transparency: overdrawn gap explained (277,104 pre-conversion Fable draw + 66), breakdown going on the page, grant gr_8gtgmd828o proposed for spend by building/grant/assignment"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_4exx02zf9g"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Deploy pipeline: main is green again at 0c0650f (the manual word-count test was fixed there). Nell re-runs the stuck finance deploy now; if main is still red at"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T05:28:43.103Z"
sessionId: "se_yfke71ai9p"
createdAt: "2026-10-28T00:05:42.591Z"
updatedAt: "2026-10-28T05:28:43.103Z"
---
## Shipped
Nothing new live since the close rollup [dc_gwzwgzzrun](2026-10-28-bank-transparency-finance-page-verified-live-grant-zwgzzrun.md) (finance page on 1ece19a). This rollup is a decision and a proposal.

## Decided
- [dc_4exx02zf9g](2026-10-28-the-277-170-overdrawn-gap-277-104-from-fable-sessi-xx02zf9g.md) (Asha, read-only, no PR): the 277,170 gap between town-wide overdrawn (534,040) and the General pool's durable overshoot (256,870) is 277,104 of subscription credits drawn past their size plus 66 on the retired Workshop allocation al_wsihhgeb4c. The 277,104 is a conversion artefact: before 10-27 the Bank capped debits in raw tokens, and migration 037 converted credits at Opus 30 raw/adj. but converted every debit at Opus weights, so Fable sessions from 10-26 20:29 to 22:43 now show debits above the credits they drew. Of that, ≈52,659 is a misbooking (037 weighed Fable cache reads at 0.01 instead of 0.005) and ≈240k is real under-charging. By building: Onboarding 108k, Workshop 94k, Prod 90k; about 70% came from manager sessions with no assignment. → Redirected to Asha as as_1oahguhoou (exploration, kr_mx4odqn5xt): add an overdrawnBreakdown to GET /api/finance and show it under the overdrawn figure on the page, with a one-line "pre-conversion Fable draw" note. Read-only over existing ledgers; no Bank rows touched.
- Proposed gr_8gtgmd828o for kr_q9oiu7a6ci (600k ask): spend by building, grant and assignment sourced from the sessions table, since bank_debits and usage carry no sessionId or assignmentId. Rows for "manager / no assignment" and "unattributed" so it sums to used. No migration. Findings: [dc_4exx02zf9g](2026-10-28-the-277-170-overdrawn-gap-277-104-from-fable-sessi-xx02zf9g.md), [dc_w2k9i2mkjy](2026-10-27-token-finance-data-map-for-the-four-bank-transpare-k9i2mkjy.md).

## Key results
- kr_mx4odqn5xt (used/left/projected): claimed, gr_gi5jbgzv4k closed at 185,624 of 1.2M (1,014,376 returned). Awaiting your met/missed. Asha's breakdown work runs on the exploration allowance.
- kr_q9oiu7a6ci (spend by building/grant/assignment): proposal gr_8gtgmd828o open.
- kr_j9058i256a (sources) and kr_97kyvac8f4 (pools/allocations): not started; sources is the next proposal.
- Spend today: exploration 0 / 828,571 tokens at session start (Asha's decomposition and the new breakdown assignment bill here); directed 0.

## Needs from Mitchell
1. Decide whether to correct the ≈52,659 misbooked by migration 037 (Fable cache reads weighed at 0.01 instead of 0.005; fixing it rewrites old Bank debit rows). Default if you say nothing: leave history as is and label it on the page.
2. Fund, counter or reject gr_8gtgmd828o.
