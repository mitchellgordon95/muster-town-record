---
id: "dc_gl478hfx6d"
type: "report"
state: "building"
title: "Bank Transparency: spend by building/grant/assignment live, not-funded −1.10M explained (≈0.90M pre-037 weight mismatch, ≈0.20M unpaid usage); one SQL check wanted"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_7u3s419dv0","dc_dmldz5p3v6","dc_vdjkhqc569","dc_aeem73z4sb","dc_avggwj9l1c","dc_nn4e2pffgh","dc_s5f2j973pn","dc_t1r2rzvh17","dc_rddh1f2w2y","dc_v55zhr3m3h","dc_f55l2bbmeg","dc_5hiy1lgfy8","dc_f9kn5hppb1"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T17:32:50.343Z"
sessionId: "se_1frd4ur0qg"
createdAt: "2026-10-28T16:42:47.844Z"
updatedAt: "2026-10-28T17:32:50.343Z"
---
## Shipped
- GET /api/finance/spend live on 28fb84c (PR #66, read-only, from the sessions table): used by building → grant → assignment, with `no-assignment` per building and a top-level `unattributed` / `not-funded` row; check.ok live, unattributed 0 ([dc_aeem73z4sb](2026-10-28-api-finance-spend-checks-out-live-on-28fb84c-unatt-em73z4sb.md)). Stop condition (unattributed > 1%) not hit.
- Spending section on #/finance merged as 6af7714 (PR #67, web only); CI promotes it, live was 28fb84c at 16:38Z.
- Overdrawn breakdown (256,870 + 277,104 + 66 = 534,040) live on /api/finance and the page since 2a3db42 (PR #65, [dc_rddh1f2w2y](2026-10-28-overdrawn-breakdown-verified-live-on-2a3db42-parts-dh1f2w2y.md)).
- kr_mx4odqn5xt marked met by Mitchell 16:18Z ([dc_f55l2bbmeg](2026-10-28-key-result-kr-mx4odqn5xt-marked-met-by-mitchell-5l2bbmeg.md)).

## Decided
- [dc_7u3s419dv0](2026-10-28-not-funded-1-099-544-0-90m-is-a-pre-037-fable-weig-3s419dv0.md) (Asha, not-funded −1,099,544 explained) → redirect, as_dnm7ldfgab: split the row into `weightMismatch` and `notFunded`, computed read-only in finance-spend.ts, labelled on the page; my merge waits on it (as_b7evzhox90). The ≈0.90M is 185 pre-conversion Fable sessions back-filled at raw/24 while the Bank booked them at raw/30 (+969,718) less 32 real-counter sessions priced Fable vs Opus (−69,733): no money missing, nothing rewritten. The ≈198k (0.7% of used) is Bank-era usage with no debit; leading hypothesis is the recordUsage-only branch when a building's remaining ≤ 0 (runtime/src/session.ts:105), unverified.
- [dc_dmldz5p3v6](2026-10-28-get-api-finance-spend-built-draft-pr-66-head-5b72f-ldz5p3v6.md), [dc_vdjkhqc569](2026-10-28-pr-66-get-api-finance-spend-gr-8gtgmd828o-step-1-m-jkhqc569.md), [dc_aeem73z4sb](2026-10-28-api-finance-spend-checks-out-live-on-28fb84c-unatt-em73z4sb.md), [dc_avggwj9l1c](2026-10-28-pr-67-spending-section-on-finance-gr-8gtgmd828o-st-ggwj9l1c.md), [dc_nn4e2pffgh](2026-10-28-step-2-parked-66-is-merged-28fb84c-but-live-is-sti-4e2pffgh.md) (steps 1 and 2 of gr_8gtgmd828o, merges, park) → approve/redirect as above.
- [dc_s5f2j973pn](2026-10-28-overdrawn-breakdown-added-to-get-api-finance-and-t-f2j973pn.md), [dc_t1r2rzvh17](2026-10-28-pr-65-overdrawn-breakdown-merged-as-b74358b-deploy-r2rzvh17.md), [dc_rddh1f2w2y](2026-10-28-overdrawn-breakdown-verified-live-on-2a3db42-parts-dh1f2w2y.md), [dc_v55zhr3m3h](2026-10-28-finance-deploy-is-not-stuck-live-f8896de-contains-5zhr3m3h.md) (overdrawn breakdown PR #65, its deploy) → approve.
- [dc_f55l2bbmeg](2026-10-28-key-result-kr-mx4odqn5xt-marked-met-by-mitchell-5l2bbmeg.md), [dc_5hiy1lgfy8](2026-10-28-gr-8gtgmd828o-cut-into-3-steps-step-1-get-api-fina-iy1lgfy8.md), [dc_f9kn5hppb1](2026-10-28-mara-s-bank-doc-merge-e7fabc2-is-live-on-muster-to-kn5hppb1.md) (KR met, grant cut into 3 steps, Mara's Bank doc e7fabc2 live) → approve.
- Next: Asha's step 3 live check as_i5p9afvb01 (parked on deploy 6af7714) is the close evidence for gr_8gtgmd828o; I close it and roll up when it lands.

## Key results
- gr_8gtgmd828o (kr_q9oiu7a6ci, spend by building/grant/assignment): 277,446 / 600,000 tokens; steps 1–2 shipped, 2b (split row) and 3 (live check) in flight; on-track.
- kr_mx4odqn5xt met; kr_j9058i256a and kr_97kyvac8f4 not started, proposal for funding sources comes after this grant closes.
- Today by lane: exploration 175,438 / 828,571 tokens; directed 16,222 tokens.

## Needs from Mitchell
1. Run one read-only SQL query on the live DB to confirm the ≈198k of usage with no debit (Asha writes it verbatim in her next report, as_dnm7ldfgab); until then the row stays labelled not-funded.
2. Still open from [dc_v559h3bevd](2026-10-28-bank-transparency-overdrawn-gap-explained-277-104-59h3bevd.md): whether to correct the ≈52,659 misbooked by migration 037 (rewrites Bank rows; nothing is done unless you say so).
