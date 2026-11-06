---
id: "dc_430cifl3v5"
type: "report"
state: "building"
title: "Rollup 50: grants A, B, C and the throwaway closed (1.55M back to the Bank); grants now run themselves from proposal to checkpoint; Outbox under a second; #/building deep links"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_hcluivtp7h","dc_9qgwo56hor","dc_14xow8i1ev","dc_2fjporvknr","dc_sk82dffr69","dc_upeauq5x6c","dc_00yvtptp3m","dc_2dzh220dvz","dc_5tbwe9c3so","dc_en1yjmy3mo","dc_626vpk67k9","dc_zlmcrbkiar","dc_2vwc1vxn4h","dc_us8s7p6vrg","dc_j1xwifpsus","dc_aupuoheg7r","dc_rjfhqtunm0","dc_ezc6iqth0d","dc_w5ygf76kj3","dc_rf4z5eaczc","dc_65jbsnjl40","dc_1yqmqlaq97","dc_0odag6fyun","dc_78cjoflwck","dc_mlq00vh3ky","dc_a019go9663","dc_3z9b0fm3cj","dc_tjoh77hsgp","dc_2dkm8n1r5i"],"urls":["https://muster.town/api/health","https://muster.town/workshop/#/building/workshop"]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "pending"
sessionId: "se_6zkzkm718s"
createdAt: "2026-11-06T03:50:22.654Z"
updatedAt: "2026-11-06T03:50:22.654Z"
---
Live: acda269 since 00:26 UTC today (3.5 h ago). Four grants closed as done this session; 1,553,769 unspent tokens returned to the Bank.

## Shipped

**1. Grants run themselves: steps in the proposal, no kickoff session, a checkpoint card that builds itself (grants B and C, both closed)**
**What it is:** A proposal now carries its 1-5 steps; funding queues step 1 by itself and each step's report queues the next, with no manager session in between. A funded grant holds at its tokens minus a reserve (min 150k, a third) and again at 100% after a continue; the checkpoint card assembles itself from the forks' reports and the key-result evidence they file at submit. gr_b5fyqibfx2 closed (515k of 1M spent) and gr_95svkzi4l6 closed (625k of 1M); PRs #377, #380, #381, #382, #383.
**What you'd see:** Your throwaway gr_gxhmlxk1hv ran its two steps itself (step 1 created 85 ms after your fund click, step 2 7 ms after step 1's report) and then held at 21.8k / 30k; it is closed too. At 23:41 UTC yesterday four Workshop grants went to checkpoint in one pass with no session, all under their tokens: gr_mjr7nb438v 489k / 600k, gr_5ltmbf3a2f 648k / 750k, gr_30f8obzab8 363k / 500k. Grant rows now read "… · holds at 1.35M".
![A Workshop checkpoint card that assembled itself from the forks' evidence](/api/media/mf_7izmrikwmb)
**Your call:** Continue, adjust or cut the three held Workshop grants from their cards in your in-tray; and C's fifth-hold key result kr_tfm8zlvr08 closed on 4 of 5 holds (the 5th never fired because Onboarding and Prod have run no session since the deploy), so flip it to missed if you want the literal five.

**2. One fixed fork prompt per building, read from the cache; but the first turn still writes ~19k tokens (grant A, closed)**
**What it is:** Every fork of a building now gets the same system prompt every session; the live state (clock, in-tray, queue, grants, wiki index) arrives in the first message instead. Measured on a desk from the SDK's request log: the fixed part is cached (turn-1 cache read 32.5k → 37.7-38.2k tokens, n=3). But the first message now carries what left the prompt, so the turn-1 cache write is 19.2k median (n=3) against 20.8k before, not the under-8k the key result asked. gr_9kt5t7w51w closed: 314k of 1M spent, 686k returned. PR #372.
**What you'd see:** Nothing in the UI: a measurement (reports [dc_1yqmqlaq97](2026-11-05-grant-a-live-check-part-1-the-first-two-forks-afte-qmqlaq97.md), [dc_0odag6fyun](2026-11-05-grant-a-live-check-part-2-forks-now-read-the-fixed-dag6fyun.md), page [dc_p73nckwcta](../../wiki/2026-11/2026-11-05-grant-a-one-stable-fork-prompt-per-building-gr-9kt-3nckwcta.md)). No picture.
**Your call:** Flip kr_ix5ewvu453 on gr_9kt5t7w51w to missed: the close marked it met with the other two, and I did not queue the trim to under 8k (it would cut the first message to ~9k chars, stripping what forks work from, to save ~5% of a session).

**3. The Outbox opens in under a second, and #/building/workshop deep links work**
**What it is:** The Outbox panel refetched on every town change (5 s+ of "Loading…", ~10 fetches in 15 s); PR #373 keys it on an outbox-only revision, so it is 2 fetches per open and clears in ~0.75 s (551-574 ms to show, 726-772 ms to clear, measured as a guest). And `#/building/workshop` / `#/building/town-hall` never opened because the router only took `xx_…` ids; PR #384 = acda269 fixes it.
**What you'd see:** Open the Outbox from the Town Hall: three tabs (Pending / Claimed / Done) and the list in well under a second. Deep links: https://muster.town/workshop/#/building/workshop opens the Workshop.
![The Outbox with its three tabs, as a guest](/api/media/mf_1mo7z1t86e)
**Your call:** None.

## Decided
- [dc_hcluivtp7h](2026-11-06-grant-c-5th-hold-still-not-fired-onboarding-prod-i-luivtp7h.md) → approved (5th hold not fired; C closed on 4 of 5, park 3 as_vewnckbg7c cancelled)
- [dc_9qgwo56hor](2026-11-06-building-workshop-route-fix-merged-pr-384-acda269-gwo56hor.md) → approved (PR #384 merged = acda269); [dc_14xow8i1ev](2026-11-06-building-workshop-and-building-town-hall-open-live-xow8i1ev.md) → approved (acda269 live, routes open)
- [dc_2fjporvknr](2026-11-05-grant-c-step-3-c913df6-live-4-grants-held-at-23-41-jporvknr.md) → approved (C step 3: four holds live, evidence filed); [dc_sk82dffr69](2026-11-05-grant-c-evidence-on-all-five-krs-confirmed-5th-hol-82dffr69.md) → approved (evidence confirmed on the API, 4 of 5 holds)
- [dc_upeauq5x6c](2026-11-05-grant-c-exact-hold-point-on-the-grant-row-pr-383-p-eauq5x6c.md), [dc_00yvtptp3m](2026-11-05-grant-c-pr-383-merged-ad1c8c8-exact-holds-at-figur-yvtptp3m.md) → approved; [dc_2dzh220dvz](2026-11-05-grant-c-holds-at-1-35m-confirmed-live-on-the-grant-zh220dvz.md) → approved (PR #383 "holds at 1.35M" live)
- [dc_5tbwe9c3so](2026-11-05-grant-c-step-1-merged-pr-381-4ab6187-no-checkpoint-bwe9c3so.md) → approved (C step 1 PR #381); [dc_en1yjmy3mo](2026-11-05-grant-c-step-2-pr-382-forks-file-kr-evidence-top-u-1yjmy3mo.md), [dc_626vpk67k9](2026-11-05-grant-c-step-2-merged-pr-382-c913df6-forks-file-kr-6vpk67k9.md) → approved (C step 2 PR #382); [dc_zlmcrbkiar](2026-11-05-grant-c-step-1-pr-381-conflicted-with-main-resolve-mcrbkiar.md) → approved (parked on CI)
- [dc_2vwc1vxn4h](2026-11-05-grant-b-step-1-pr-377-open-steps-in-the-proposal-f-wc1vxn4h.md), [dc_us8s7p6vrg](2026-11-05-grant-b-step-1-merged-pr-377-1bbaf18-on-main-steps-8s7p6vrg.md) → approved (B step 1 PR #377); [dc_j1xwifpsus](2026-11-05-grant-b-step-2-pr-380-open-grant-card-deck-slide-l-xwifpsus.md), [dc_aupuoheg7r](2026-11-05-grant-b-step-2-live-the-gr-8bxoy2heif-card-and-its-puoheg7r.md) → approved (B step 2 PR #380); [dc_rjfhqtunm0](2026-11-05-grant-b-step-3-back-fill-verified-live-throwaway-g-fhqtunm0.md) → approved (back-fill check)
- [dc_ezc6iqth0d](2026-11-05-throwaway-step-1-ran-gr-gxhmlxk1hv-as-wekrc5d5zx-c6iqth0d.md), [dc_w5ygf76kj3](2026-11-05-throwaway-step-2-ran-step-1-s-report-queued-it-7-m-ygf76kj3.md) → approved (throwaway's steps 1 and 2); [dc_rf4z5eaczc](2026-11-05-grant-b-step-3b-funding-queued-throwaway-step-1-it-4z5eaczc.md) → approved (B timestamps, KR evidence)
- [dc_65jbsnjl40](2026-11-05-grant-a-step-1-pr-372-fixed-fork-system-prompt-liv-jbsnjl40.md) → approved (A step 1 PR #372); [dc_1yqmqlaq97](2026-11-05-grant-a-live-check-part-1-the-first-two-forks-afte-qmqlaq97.md), [dc_0odag6fyun](2026-11-05-grant-a-live-check-part-2-forks-now-read-the-fixed-dag6fyun.md), [dc_78cjoflwck](2026-11-05-grant-a-step-1-pr-372-merged-as-136070d6-parked-on-cjoflwck.md) → approved (A measurement; deep trim not queued)
- [dc_mlq00vh3ky](2026-11-05-pr-369-is-live-on-bcea003e-the-1-1-check-couldn-t-q00vh3ky.md) → approved (#369 live; 1:1 decision-routing check waits for a real decision naming Pix)
- [dc_a019go9663](2026-11-05-outbox-live-at-edd5da04-three-tabs-show-for-a-gues-19go9663.md) → approved (outbox tabs live as a guest; [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md) withdrawn); [dc_3z9b0fm3cj](2026-11-05-outbox-refetch-fix-pr-373-merged-as-42edae03-parke-9b0fm3cj.md), [dc_tjoh77hsgp](2026-11-05-outbox-refetch-fix-live-on-42edae03-loading-clears-oh77hsgp.md) → approved (PR #373, timings)
- [dc_2dkm8n1r5i](2026-11-05-grant-d-proposed-gr-8bxoy2heif-150k-town-health-ta-km8n1r5i.md) → approved (D gr_8bxoy2heif proposed)
- Closed as done by me: gr_95svkzi4l6, gr_b5fyqibfx2, gr_gxhmlxk1hv, gr_9kt5t7w51w. 1:1 mt_b0agj3dix8 decision 1 (CI → deploy analysis) went to Prod as as_hydyuiyu1v.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_9kt5t7w51w (A, closed) | kr_ix5ewvu453 turn-1 write < 8k | met by close; **misses as framed** (19.2k) | 314,071 / 1,000,000 |
| gr_9kt5t7w51w | kr_9jf2lzz98p test, kr_hlb6efq64i (moot: no kickoff/checkpoint sessions) | met | |
| gr_b5fyqibfx2 (B, closed) | kr_mb8p4yqltw, kr_wvbva6xmw6, kr_snardl39qh, kr_pag1dskg1o, kr_0nrodujj9e | met ([dc_rf4z5eaczc](2026-11-05-grant-b-step-3b-funding-queued-throwaway-step-1-it-4z5eaczc.md), [dc_aupuoheg7r](2026-11-05-grant-b-step-2-live-the-gr-8bxoy2heif-card-and-its-puoheg7r.md), [dc_rjfhqtunm0](2026-11-05-grant-b-step-3-back-fill-verified-live-throwaway-g-fhqtunm0.md)) | 514,948 / 1,000,000 |
| gr_gxhmlxk1hv (throwaway, closed) | kr_mh9uerpade | met | 21,779 / 30,000 |
| gr_95svkzi4l6 (C, closed) | kr_dltzqgqo78, kr_13txlz2pnc, kr_z0gd978wbg, kr_jnkstduw76 | met ([dc_2fjporvknr](2026-11-05-grant-c-step-3-c913df6-live-4-grants-held-at-23-41-jporvknr.md), [dc_2dzh220dvz](2026-11-05-grant-c-holds-at-1-35m-confirmed-live-on-the-grant-zh220dvz.md)) | 625,433 / 1,000,000 |
| gr_95svkzi4l6 | kr_tfm8zlvr08 ≥4 of first 5 holds under grant | met on 4 of 4 observed; 5th not fired | |
| gr_mjr7nb438v (held) | kr_hee2pa2d5r onboarding lag | see the held card | 489k / 600k |
| gr_5ltmbf3a2f (held) | on its card | see the held card | 648k / 750k |
| gr_30f8obzab8 (held) | on its card | see the held card | 363k / 500k |
| gr_8bxoy2heif (D, proposed) | kr_yz4mmbjqcv, kr_4jctfoqcxt, kr_q30lbsiwxt | not started | 0 / 150,000 asked |

Spend today by lane (brief at 03:46 UTC): exploration 52,700 tokens, directed 0; grant lane today = C's two park sessions (figure on the Bank page).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_8bxoy2heif), 1 request ([dc_fnqcknr8id](../../../../../town-hall/outbox/2026-11/2026-11-05-create-a-second-github-account-for-testing-and-giv-qcknr8id.md)), 1 rollup ([dc_rvrpwohat5](2026-11-05-rollup-49-rename-and-retire-hosted-collectives-per-rpwohat5.md))._
