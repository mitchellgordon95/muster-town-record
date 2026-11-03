---
id: "dc_7lpbltjy1j"
type: "wiki"
state: "building"
title: "Rollup 37 materials"
authorId: "ag_d40g4tqsz5"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-10-31T22:43:14.504Z"
updatedAt: "2026-11-03T19:11:54.462Z"
---
Archive (items 1-17, Decided since rollup 36, all covered by rollups 37 [dc_zcuri3xdk2](../../report/2026-11/2026-11-02-workshop-rollup-37-checkpoint-of-the-hosted-collec-uri3xdk2.md) and 38 [dc_e5ymrwlhrv](../../report/2026-11/2026-11-02-workshop-rollup-38-goal-editor-long-names-and-haik-ymrwlhrv.md)): [dc_0q9nlk7fa3](../../note/2026-11/2026-11-03-rollup-materials-archive-rollups-1-38-9nlk7fa3.md). Older prose: this page's revisions (GET /api/docs/dc_7lpbltjy1j).

Rolled up (one line each; details in the rollup):
- 18. Ask-only rollups fold into the grant's in-tray row (#265, #270, #272 = 335c586 LIVE in 6e6d663, not yet live-checked: as_fztoul7292 held, no free tokens): rollup 39 [dc_6fnguvuqgu](../../report/2026-11/2026-11-03-workshop-rollup-39-go-fund-gr-xxx-asks-sit-on-the-nguvuqgu.md) item 1.
- 19. Checkpoint card shows evidence and the real overspend (#266, #271): rollup 39 item 2.
- 20. Exploration caps combine as the minimum; explorers read §7-8 first (gr_yu6qw3j9x5 step 1, #273 = 0449018, live-checked [dc_sisyjg8e7m](../../report/2026-11/2026-11-03-live-check-0449018-gr-yu6qw3j9x5-step-1-live-evide-syjg8e7m.md)): rollup 40 item 2.
- 22. A captain steers the buildings under their goal from the web (gr_zsm1piyqyx, #259 = 38d7785 + #277 = 575ee2d; grant CLOSED as done 2026-11-03 by the manager, 500,164 / 500,000 spent): rollup 40 item 1 (the grant's close report), picture mf_7nq2r0jm12.
- 23. desksTotal on a captained goal (gr_yu6qw3j9x5 step 2, #278 = e3300795 + #282 = 66e5d33; grant closed as done by the manager 11-03): rollup 41 [dc_5tmsmnw12h](../../report/2026-11/2026-11-03-workshop-rollup-41-gr-yu6qw3j9x5-closed-as-done-a-msmnw12h.md), picture mf_s126yqmqji.

Rollup 42 candidates. Mark LIVE only after a health-commit check. Live at 19:10:27Z 11-03 (GET /api/health, read by Pix 2 as_w2j469399g, server started 19:09:58Z): ae3c410 (contains 227906a, 66e5d33 and #280 = ae3c410).

## Shipped candidates

**21. A human can stop a funded grant; the town winds it down** (gr_8i952perny steps 1+2, kr_ghexd88frr, kr_4s0ccmvtsp, kr_kaz3nj127k, kr_f46tddd9as; 1:1 mt_a6wb51enia)
- PRs: step 1 #275 = 227906a; step 2 #280 = ae3c410 (merged by Pix 1 as_yn9zzmm864 at CI-green head 323b62f). **Both LIVE in ae3c410** (health 19:10:27Z 11-03).
- Live check without a stop (Pix 2 as_w2j469399g, after 19:10:27Z 11-03): GET /api/buildings/town-hall/intray has the `stopped` key (empty list); the live web bundle main-BFv18DXS.js has the "Stop grant…" button (title "…with a reason", confirm disabled while the reason is blank), the "stopping"/"Stopping: a human stopped it…" labels and "Stopped: for the record". gr_ikgaundf5p is still `proposed` (0 spent); Bank freeTokens 0 (general 2,191,974, open asks 1,310,000).
- Evidence per KR (tests): kr_ghexd88frr server grants.test.ts (human 200, manager stop 403, manager close-stopped 403, withdraw 200); kr_4s0ccmvtsp core grant-stop.test.ts (fork interrupted, queued cancelled, stopping → stopped); kr_kaz3nj127k core tests (pool: free +unspent; member input unchanged 460,000); kr_f46tddd9as server test (KRs missed with note) + #280's in-tray `stopped` and deck-slide tests.
- STILL TO DO, needs Mitchell: fund gr_ikgaundf5p (5,000) in the Town Hall in-tray, then press "Stop grant…" on its row with any reason. Then a session reads GET /api/bank + Bank page, GET /api/grants/gr_ikgaundf5p (kr_una0o5bucs missed "Grant stopped: <reason>"), the manager's system message, and takes the ≤300 px picture of the "Stopped: for the record" row. Note: funding is not blocked at freeTokens 0 (grants.ts fund only adds an overdraft note), but with the pool overdrawn freeTokens may read 0 both before and after the stop; compare free.fundedRemainingTokens (1,068,022 after 19:10:27Z) drop by the unspent rest, not only freeTokens.
- Picture: none yet.
- **What it is:** a human who can fund a grant (or its goal's captain) presses "Stop grant…" on a funded or checkpoint grant with a reason (POST /api/grants/:id/stop; a manager gets 403). The grant goes to "stopping": running forks wrap up, queued work is cancelled, open key results are missed with the reason, the manager is told; when no session runs on it it closes as stopped and the unspent rest goes back (pool: free tokens; member-funded: stays on the input). The in-tray and review deck show it for the record until 3 days after it closes (who, why, spent of granted, where the rest went); not counted in the badge.
- **What you'd see:** Town Hall in-tray: a funded grant's row has "Stop grant…"; after stopping, a "Stopped: for the record" section with a red "stopped" pill, "Mitchell stopped it: <reason>" and "spent X of Y; Z unspent returned to the Bank as free tokens"; Review as deck has its slide.
- **Your call:** fund gr_ikgaundf5p, then press "Stop grant…" on it with any reason.

## Decided since rollup 39 (all approved; covered by rollup 40)
- [dc_s6qzn3hngy](../../report/2026-11/2026-11-03-pr-273-merged-as-0449018-caps-minimum-on-path-expl-qzn3hngy.md), [dc_2875zs7syw](../../report/2026-11/2026-11-03-pr-259-merged-as-38d7785-captain-steering-gates-re-75zs7syw.md), [dc_z8mnleg08h](../../report/2026-11/2026-11-03-gr-8i952perny-step-1-grants-stop-in-draft-pr-275-c-mnleg08h.md), [dc_sisyjg8e7m](../../report/2026-11/2026-11-03-live-check-0449018-gr-yu6qw3j9x5-step-1-live-evide-syjg8e7m.md), [dc_3sdefshj78](../../report/2026-11/2026-11-03-gr-zsm1piyqyx-step-2-captainof-on-api-me-talk-to-p-defshj78.md), [dc_6s0184hhvv](../../report/2026-11/2026-11-03-pr-275-merged-as-227906a-human-only-stop-of-a-fund-0184hhvv.md), [dc_cv7nfx5egs](../../report/2026-11/2026-11-03-gr-zsm1piyqyx-step-2-pr-277-re-merged-with-main-ci-7nfx5egs.md), [dc_q830bdkas2](../../report/2026-11/2026-11-03-gr-yu6qw3j9x5-step-2-goals-deskstotal-in-draft-pr-30bdkas2.md), [dc_va3ezq271h](../../report/2026-11/2026-11-03-pr-277-merged-as-575ee2d-captain-steering-in-the-w-3ezq271h.md).

## Decided since rollup 40
- [dc_0wjjb3i6ks](../../report/2026-11/2026-11-03-pr-278-merged-as-e3300795-desks-per-subtree-redepl-jjb3i6ks.md) (Pix 1: #278 merged as e3300795, KR verdicts), [dc_wdrq268xfl](../../report/2026-11/2026-11-03-pr-280-conflicted-with-main-re-merged-at-323b62f-c-rq268xfl.md) (Pix 2: #280 re-merged at 323b62f, parked on CI), [dc_u0c2qj4prj](../../report/2026-11/2026-11-03-gr-yu6qw3j9x5-follow-up-desk-totals-now-hold-a-nam-c2qj4prj.md) (Pix 3: #282 merged as 66e5d33, claimDesk grow gated); all approved.

## Decided since rollup 41
- [dc_inj8i45d10](../../report/2026-11/2026-11-03-pr-280-merged-as-ae3c410-stop-grant-in-the-web-red-j8i45d10.md) (Pix 1: #280 merged as ae3c410, approved).
