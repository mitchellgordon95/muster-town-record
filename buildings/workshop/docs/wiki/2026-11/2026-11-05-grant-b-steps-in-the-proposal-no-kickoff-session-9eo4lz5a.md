---
id: "dc_lq9eo4lz5a"
type: "wiki"
state: "building"
title: "Grant B: steps in the proposal, no kickoff session"
authorId: "ag_l6074j0t7y"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-05T21:51:03.265Z"
updatedAt: "2026-11-05T23:18:10.377Z"
---
State 2026-11-05 (Pix 1, as_160so3wz5o, grant gr_b5fyqibfx2). Source: Mitchell 1:1 mt_y949h9jto6; cutover rule mt_stsjh68yz2 decision 1 (no fallback paths).

**Step 1 LIVE: PR #377 = 1bbaf18** (report [dc_2vwc1vxn4h](../../report/2026-11/2026-11-05-grant-b-step-1-pr-377-open-steps-in-the-proposal-f-wc1vxn4h.md)). Schema `GrantStep`, `Grant.steps`, `Assignment.grantStep`; migration 096 back-fills open proposals; fund → `Grants.queueStep(g,0)`; `queueNextStep` on a non-pivot report; stop/redirect cancels the queued next step. Tests core/test/grant-steps.test.ts.

**Step 2 LIVE: PR #380 = 142e85c.** Card + deck slide list numbered steps (mf_x1rehoutf0, [dc_aupuoheg7r](../../report/2026-11/2026-11-05-grant-b-step-2-live-the-gr-8bxoy2heif-card-and-its-puoheg7r.md)). kr_snardl39qh evidence done.

**Step 3 DONE (live at 142e85c), all KR evidence in hand:**
- kr_wvbva6xmw6: all 8 open proposals have exactly 1 step, no funded grant back-filled ([dc_rjfhqtunm0](../../report/2026-11/2026-11-05-grant-b-step-3-back-fill-verified-live-throwaway-g-fhqtunm0.md)).
- kr_mb8p4yqltw: throwaway gr_gxhmlxk1hv funded by Mitchell (us_1la74k332n) at 23:15:50.694Z; step 1 as_wekrc5d5zx created 23:15:50.779Z (event 134792, queue building, lane grant, createdBy = the funder, fromReportId null) inside the fund request. No "Grant … funded" assignment; no Pix session between 23:15:26.730Z (se_t40olsuf29 ended) and 23:15:59.895Z (se_we6j20pf2j, after step 2 existed). Report of the check: as_160so3wz5o.
- kr_pag1dskg1o / kr_mh9uerpade: step 1 report [dc_ezc6iqth0d](../../report/2026-11/2026-11-05-throwaway-step-1-ran-gr-gxhmlxk1hv-as-wekrc5d5zx-c6iqth0d.md) 23:15:59.828Z → step 2 as_9xph9txj9c created 23:15:59.835Z by system (fromReportId [dc_ezc6iqth0d](../../report/2026-11/2026-11-05-throwaway-step-1-ran-gr-gxhmlxk1hv-as-wekrc5d5zx-c6iqth0d.md)). Report [dc_w5ygf76kj3](../../report/2026-11/2026-11-05-throwaway-step-2-ran-step-1-s-report-queued-it-7-m-ygf76kj3.md).
- Throwaway spent 21,779 / 30,000 (2 sessions: se_66r4sb4r7n 9,717, se_1mnfen56tf 12,062).

**Next:** Pix closes gr_gxhmlxk1hv and gr_b5fyqibfx2 (close_grant) in the next rollup. Continuation as_ag35xoj65d (waits 2026-11-06 12:00Z) is now redundant: cancel it.

**Known cosmetic:** back-filled step titles are cut mid-word at 160 chars.
