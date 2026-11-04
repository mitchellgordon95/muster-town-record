---
id: "dc_5tmsmnw12h"
type: "report"
state: "building"
title: "Workshop rollup 41: gr_yu6qw3j9x5 closed as done, a captained goal can cap the desks under it; live on 66e5d33"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_0wjjb3i6ks","dc_wdrq268xfl","dc_u0c2qj4prj","dc_d8ccuil7w1","dc_6zmwm2bse5"],"urls":["https://muster.town/api/health","https://github.com/mitchellgordon95/muster-town/pull/278","https://github.com/mitchellgordon95/muster-town/pull/282"]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Key results are no longer marked met or missed by a human: when a grant closes as done its key results go to met on their own, the met/missed rows leave the Tow"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T00:20:18.308Z"
sessionId: "se_ytfnknibuv"
createdAt: "2026-11-03T18:03:12.124Z"
updatedAt: "2026-11-04T00:20:18.308Z"
---
Live 66e5d33 (GET /api/health 18:00:13Z, server started 04:17:48Z). It contains PR #278 = e3300795 and PR #282 = 66e5d33 (the item below) and the pipe-free ask lines of rollup 39 (335c586, now live-checked). This rollup is the close report of gr_yu6qw3j9x5. Not in it yet: PR #280 (web half of "stop a funded grant", Pix 1 merging now) and PR #274 (trim of the rollup materials page, Pix 2 merging now); both come next time. A redeploy is queued behind this session.

## Shipped

**1. A captained goal can cap the desks under it. Grant gr_yu6qw3j9x5 closed as done**
**What it is:** From our 1:1 mt_a6wb51enia: a subtree is throttled by desks and the exploration cap, never by a per-captain budget. Migration 086 adds goals.desksTotal; an admin or a captain above sets it, and a captain can't set it past the total above them. The total in force is the smallest on the path to the root (GET /api/goals funding.desksTotal). Raising a building's headcount, creating or attaching a building, or a named resident joining a full lab past any total on the path answers 409 "Desk total reached: … can have at most N, not M", admins included. PR #278 = e3300795 (Pix 1, [dc_0wjjb3i6ks](2026-11-03-pr-278-merged-as-e3300795-desks-per-subtree-redepl-jjb3i6ks.md)) and PR #282 = 66e5d33 (Pix 3, [dc_u0c2qj4prj](2026-11-03-gr-yu6qw3j9x5-follow-up-desk-totals-now-hold-a-nam-c2qj4prj.md)); step 1 (#273, caps combine as the minimum, explorer brief names §7-8) shipped in rollup 40. I closed the grant with all three key results claimed: kr_h0pqsgkov8 is now live-proven (the two "Explore under …" assignments created at 17:59:51Z, as_mqndszybbd and as_686vcc6kc2, name §7-8); kr_86wt7nnrfg is live (cap line names gl_town) with the minimum rule proven by core free-tokens.test.ts:61-64; kr_jya7n4g88a is live in the API (desksTotal on all 22 goals, null everywhere) with the 409 and the "Desks: N of M" line proven by core desks-total.test.ts, server rest.test.ts and web desksLine.test.ts, not yet live because no total is set. Spent 407,005 of 500,000 tokens; 92,995 returned to the Bank. One gap left, noted in docs/goals.md: moving or retiring a goal re-parents its buildings without re-checking the new ancestors' total.
**What you'd see:** Goal tree → a captained goal's detail → a "Desk total" field and the line "Desks: N of M (set on goal X)". Picture from the mock dev server, since no live total is set.
![Goal detail with a Desk total field and the Desks: N of M line](/api/media/mf_s126yqmqji)
**Your call:** mark the three key results met or missed on the grant's row; to see it live first, set a Desk total (e.g. 3) on gl_bl_t7slw19vgg, then raise UI / UX's desks past it and expect the 409 and the "Desks: N of M" line.

## Decided
- [dc_0wjjb3i6ks](2026-11-03-pr-278-merged-as-e3300795-desks-per-subtree-redepl-jjb3i6ks.md) → approve (PR #278 merged as e3300795; the three KR verdicts; close waited on the deploy).
- [dc_wdrq268xfl](2026-11-03-pr-280-conflicted-with-main-re-merged-at-323b62f-c-rq268xfl.md) → approve (PR #280 re-merged with main at 323b62f, parked on CI; its continuation runs now).
- [dc_u0c2qj4prj](2026-11-03-gr-yu6qw3j9x5-follow-up-desk-totals-now-hold-a-nam-c2qj4prj.md) → approve (PR #282 merged as 66e5d33: a named resident joining a full lab is held under the total; redeploy queued).
- [dc_d8ccuil7w1](2026-11-03-335c586-live-checked-gr-58n37j410s-s-ask-has-no-pi-ccuil7w1.md) → approve (335c586 live-checked: no pipes in any of the 11 in-tray ask lines).
- [dc_6zmwm2bse5](2026-11-03-gr-yu6qw3j9x5-ready-to-close-all-3-krs-claimable-l-mwm2bse5.md) → approve (Pix 4's close evidence; a fork can't close_grant, so I closed it here; bookkeeping queued as as_ndp832w7lz).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_yu6qw3j9x5 captained subtree throttled by desks and cap | kr_h0pqsgkov8 explorer brief names §7-8 (11-05) | claimed, closed done (this rollup) | 407,005 / 500,000 (92,995 returned) |
| | kr_86wt7nnrfg caps combine as the minimum (11-06) | claimed | |
| | kr_jya7n4g88a desksTotal on a captained goal (11-08) | claimed | |
| gr_8i952perny stop a funded grant | kr_ghexd88frr human-only stop (11-06) | on-track (server side live in 227906a; web PR #280 merging now) | 403,591 / 500,000 (18:0xZ) |
| | kr_4s0ccmvtsp wind-down first (11-07) | on-track (in 227906a) | |
| | kr_kaz3nj127k money back (11-07) | on-track (live Bank check needs a funded throwaway grant stopped by you) | |
| | kr_f46tddd9as KRs missed, in-tray row, manager told (11-08) | on-track (in-tray row and deck slide in PR #280) | |
| gr_bwm0iz7rwl ask to captain a goal | kr_j1w17nw178, kr_07d30db2bf, kr_fd3ac479eb, kr_917dc5ba6d | not-started (no session since rollup 38) | 389,833 / 600,000 |
| gr_mjr7nb438v onboarding lag (goal gl_bl_hzjw0z0zlz) | kr_hee2pa2d5r onboarding material ≤ 24 h behind main for 7 days | on-track (next sweep 19:00 UTC today, sc_nx8bwd5e5o); kr_a9a473b0f8 claimed, kr_df6a5cf736 and kr_c2989de971 at-risk | 445,387 / 600,000 |

Today's spend by lane: exploration 35,547 tokens (free under the goal: 22,753), directed 112,486 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_eh6f1dl69n, gr_ikgaundf5p), 0 requests, 3 rollups ([dc_e5ymrwlhrv](2026-11-02-workshop-rollup-38-goal-editor-long-names-and-haik-ymrwlhrv.md), [dc_6fnguvuqgu](2026-11-03-workshop-rollup-39-go-fund-gr-xxx-asks-sit-on-the-nguvuqgu.md), [dc_yps0luloaj](2026-11-03-workshop-rollup-40-gr-zsm1piyqyx-closed-as-done-a-s0luloaj.md))._
