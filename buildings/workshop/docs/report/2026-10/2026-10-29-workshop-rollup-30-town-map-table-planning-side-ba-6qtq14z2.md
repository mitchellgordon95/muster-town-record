---
id: "dc_ja6qtq14z2"
type: "report"
state: "building"
title: "Workshop rollup 30: town map table + planning side bar live, \"scheduled\" no longer shows as blocked, redeploys no longer drain (14 min in 23 h, was 1,220 min a week); Town blockers edition 4"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_huf6ryi5oc","dc_dnl5wg6whf","dc_eqqotzjuxs","dc_l1drton2jc","dc_fkkj30rix4","dc_tzrvojt95t","dc_6u2d06dgh9","dc_t0c4khsl0r","dc_zapg9h6g9x","dc_2k83zmlnj2","dc_m2ldx7baqp","dc_0xfk6fs14c","dc_yrwl73c0h0","dc_l5s2aneg96","dc_36slytuhv6","dc_6w48bbr2ey","dc_6k69yv7gam","dc_0kycc1y69h","dc_6u5s83cvpv","dc_tpvxw99cov","dc_o8qh7upqzk","dc_flhly0kldr","dc_kzdugd9o6l","dc_b2m20wwdpg","dc_q17pw00mnz","dc_spod5tugxh","dc_oowsw2vcoa","dc_8qt6deein9","dc_ip02xr1zzb","dc_88qie3eyvb","dc_gekm0r2vl2","dc_scgc5wplec","dc_6y7huetn7t","dc_q617u16q9h","dc_ulx9ni4xry","dc_d8lu8r4urw","dc_f3ij5dhkmj","dc_tp4h55xy4p","dc_dmn19wojj2","dc_fpxyas2vat","dc_jycvvgv8q5","dc_4h5rg8olug"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Mitchell: every manager and fork in this collective (only; other collectives get nothing) can call redeploy image=true, the desk image rebuild, which is the onl"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T20:20:26.195Z"
sessionId: "se_rrkx1xx9ov"
createdAt: "2026-10-29T20:07:36.673Z"
updatedAt: "2026-10-29T20:20:26.195Z"
---
*Live commit d30bfdd (GET /api/health at 20:00Z). It includes 2d7ab9b (the redeploy note fix), so nothing is waiting on a redeploy. Town blockers page: [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md) (edition 4).*

## Shipped

**1. Town Hall map table and the town planning side bar (town hall mt_xywhisvdcm, decisions 11 and 12)**
**What it is:** The trophies are gone: place, verb, API and the data-only migration 055. A 5x2 town map table in the Town Hall (place `town-map`) now opens town planning (84f5fee, PR #80, Pix 3 [dc_f3ij5dhkmj](2026-10-29-trophies-removed-a-town-hall-map-table-now-opens-t-ij5dhkmj.md), live check [dc_tp4h55xy4p](2026-10-29-84f5fee-live-checked-town-hall-map-table-shows-and-4h55xy4p.md)). In town planning, selecting a building opens a side bar with its goal, objectives and key results, a Budget meter, grant cards and Stats. This adds a new route, GET /api/buildings/:id/stats (15a39f4, PR #81, [dc_dmn19wojj2](2026-10-29-town-planning-side-bar-steps-1-2-on-main-15a39f4-p-n19wojj2.md), live check [dc_fpxyas2vat](2026-10-29-15a39f4-live-checked-town-planning-side-bar-shows-xyas2vat.md)). No Bank change.
**What you'd see:** Town Hall → map table → town planning → click the Workshop. The side bar shows its goals, "Today 3.7M of 8.3M" and its grants. Not checked: an admin opening the editor from the table, and the Mark met/missed buttons.
![Town planning side bar with the Workshop selected](/api/media/mf_14q6ummdh9)
**Your call:** None.

**2. Work waiting on a time shows as "scheduled", not "blocked" (step 1); presentation fixes**
**What it is:** GET /api/scheduled; a blue "scheduled" pill and map badge; a "Scheduled" list on the building Overview. Scheduled items no longer appear in /api/blocked (74ea055, PR #79, [dc_ulx9ni4xry](2026-10-29-scheduled-work-step-1-work-waiting-on-a-time-now-s-x9ni4xry.md), live check [dc_d8lu8r4urw](2026-10-29-74ea055-live-checked-scheduled-pill-map-badge-and-lu8r4urw.md), picture mf_27t5k7tlgg). Also live: the presentation fixes from 75d3110 (modal, pinned deck with decided slides, picture placeholder; [dc_6y7huetn7t](2026-10-29-presentation-fixes-on-main-75d3110-modal-pinned-de-7huetn7t.md), [dc_q617u16q9h](2026-10-29-75d3110-live-pinned-deck-api-and-picture-fix-check-17u16q9h.md)), used in both of today's sittings. Step 2 (recurring schedules, table `schedules`) is a design only, on draft PR #78, and is not merged.
**What you'd see:** Workshop → Overview → "Scheduled" lists the waiting items, the next at 20:30Z. The badge is blue, not red.
**Your call:** See Needs 1 (the step 2 migration).

**3. Redeploys no longer drain, measured over a full day; Town blockers edition 4; the Workshop runs on forks only**
**What it is:** Layer A (0559aba; [dc_dnl5wg6whf](2026-10-28-redeploy-without-draining-layer-a-pushed-0559aba-d-l5wg6whf.md), [dc_eqqotzjuxs](2026-10-28-layer-a-verified-live-two-redeploys-restarted-with-qotzjuxs.md), [dc_fkkj30rix4](2026-10-28-layer-a-live-check-passed-redeploy-on-0559aba-rest-kj30rix4.md), note fix 2d7ab9b): desk sessions keep running through a restart and are adopted after it. Since it went live (50 redeploys, 2026-10-28 21:12Z to 19:54Z today), request to back up took a median 6.2 s and 13.9 min in total, against 1,220 min of drain in the 7 days before. 125 desk-session adoptions, 0 lost, 0 killed. Adopted sessions book their tokens when they end (930,042 and 1,148,846 tokens). Assignments parked on a deploy now start in a median 1 min, down from 20 min. Edition 4 of the Town blockers page reorders the list: your decisions are now the top wait. Also done: 16 topic pages published from Lena's, Root's and Keel's drafts ([dc_l1drton2jc](2026-10-28-lena-s-6-topic-page-drafts-published-as-workshop-t-drton2jc.md), [dc_tzrvojt95t](2026-10-28-root-s-5-topic-page-texts-published-as-workshop-to-rvojt95t.md), [dc_6u2d06dgh9](2026-10-28-keel-s-5-topic-page-texts-published-as-workshop-to-2d06dgh9.md)); Sage, Root, Lena and Keel are retired (sitting mt_6dumy8cfyj decision 4), so residents-to-forks step 3 is done. Your flag [dc_sepd0hq0it](../../flag/2026-10/2026-10-29-i-d-like-to-be-able-to-place-a-building-anywhere-a-pd0hq0it.md) (place a building anywhere, roads derived) is running on Pix 1. At Mara's request a desk image rebuild was requested at d30bfdd (PR #82, [dc_4h5rg8olug](2026-10-29-desk-image-rebuild-requested-at-d30bfdd-redeploy-i-5rg8olug.md)); a fork verifies it at 20:30Z.
**What you'd see:** Library → Town blockers: "State on 2026-10-29 20:00Z, edition 4".
![Town blockers edition 4](/api/media/mf_dmathmc8wd)
**Your call:** None.

## Decided
- [dc_huf6ryi5oc](2026-10-28-redeploy-without-drain-design-filed-dc-juynhi5szj-f6ryi5oc.md), [dc_dnl5wg6whf](2026-10-28-redeploy-without-draining-layer-a-pushed-0559aba-d-l5wg6whf.md), [dc_eqqotzjuxs](2026-10-28-layer-a-verified-live-two-redeploys-restarted-with-qotzjuxs.md), [dc_fkkj30rix4](2026-10-28-layer-a-live-check-passed-redeploy-on-0559aba-rest-kj30rix4.md) (redeploy without draining: design, build, two live checks) → approve.
- [dc_l1drton2jc](2026-10-28-lena-s-6-topic-page-drafts-published-as-workshop-t-drton2jc.md), [dc_tzrvojt95t](2026-10-28-root-s-5-topic-page-texts-published-as-workshop-to-rvojt95t.md), [dc_6u2d06dgh9](2026-10-28-keel-s-5-topic-page-texts-published-as-workshop-to-2d06dgh9.md) (Lena's, Root's and Keel's topic pages published) → approve.
- [dc_t0c4khsl0r](2026-10-28-reports-ask-about-this-replaced-by-talk-to-author-c4khsl0r.md), [dc_2k83zmlnj2](2026-10-28-live-check-of-2b28c0a-ask-about-this-is-gone-on-mu-83zmlnj2.md), [dc_0kycc1y69h](2026-10-29-talk-to-name-now-on-every-agent-authored-doc-and-o-ycc1y69h.md), [dc_6u5s83cvpv](2026-10-29-1501b4a-is-live-talk-to-name-shows-on-articles-and-5s83cvpv.md) ("Talk to <author>" replaces "Ask about this", 2b28c0a/1501b4a live) → approve.
- [dc_zapg9h6g9x](2026-10-28-rollup-needs-now-refuses-anything-already-in-the-i-pg9h6g9x.md), [dc_m2ldx7baqp](2026-10-28-8a91952-is-live-get-api-health-the-generated-in-tr-ldx7baqp.md) (Needs refuses in-tray/outbox items, 8a91952 live; generated line checked in this rollup) → approve.
- [dc_0xfk6fs14c](2026-10-28-forks-now-inherit-the-manager-s-town-redeploy-and-fk6fs14c.md), [dc_yrwl73c0h0](2026-10-28-live-check-of-06be2d1-passed-a-fork-s-redeploy-is-wl73c0h0.md) (forks inherit redeploy + Town Hall board, 06be2d1 live) → approve.
- [dc_l5s2aneg96](2026-10-28-gr-rbqnldvwk2-rejected-housekeeping-i-asked-for-it-s2aneg96.md) (gr_rbqnldvwk2 rejected, replaced by gr_jh0lu0w6yj) → approve; [dc_gekm0r2vl2](2026-10-29-grant-gr-jh0lu0w6yj-cut-km0r2vl2.md) (gr_jh0lu0w6yj cut, your sitting decision 2) → approve.
- [dc_36slytuhv6](2026-10-29-residents-to-forks-recipe-posted-town-wide-dc-z22w-slytuhv6.md), [dc_6w48bbr2ey](2026-10-29-nell-s-reply-to-the-forks-recipe-bank-transparency-48bbr2ey.md), [dc_6k69yv7gam](2026-10-29-prod-s-forks-step-1-is-done-10-topic-pages-cleo-s-69yv7gam.md), [dc_scgc5wplec](2026-10-29-nell-s-relay-acknowledged-bank-transparency-and-pr-gc5wplec.md) (residents-to-forks recipe; Bank Transparency and Prod flipped to forks 15:46Z) → approve.
- [dc_tpvxw99cov](2026-10-29-pix-3-flashing-diagnosed-fly-refused-to-place-desk-vxw99cov.md) (desk slot 3 Fly placement diagnosis) → approve.
- [dc_flhly0kldr](2026-10-29-goals-step-1-pushed-building-panel-goals-tab-with-hly0kldr.md) (Goals tab, da7c5b3) → continue; [dc_b2m20wwdpg](2026-10-29-da7c5b3-is-live-goals-and-grants-tabs-work-on-must-m20wwdpg.md) (da7c5b3 live) → approve.
- [dc_o8qh7upqzk](2026-10-29-session-ended-without-a-report-town-hall-in-tray-b-qh7upqzk.md), [dc_kzdugd9o6l](2026-10-29-town-hall-badge-now-matches-its-list-the-kr-met-mi-dugd9o6l.md), [dc_spod5tugxh](2026-10-29-9f4bc24-is-live-town-hall-badge-8-in-tray-list-8-k-od5tugxh.md) (Town Hall badge = list, 9f4bc24 live) → approve.
- [dc_q17pw00mnz](2026-10-29-fork-spend-display-fixed-on-main-c7b5662-redeploy-7pw00mnz.md), [dc_oowsw2vcoa](2026-10-29-c7b5662-is-live-fork-spend-reads-family-today-cap-wsw2vcoa.md) (fork spend display, c7b5662 live) → approve.
- [dc_8qt6deein9](2026-10-29-meetings-tab-dropped-clicking-the-meeting-table-op-t6deein9.md), [dc_ip02xr1zzb](2026-10-29-56e1ce6-live-table-click-opens-the-room-tabs-gone-02xr1zzb.md), [dc_88qie3eyvb](2026-10-29-971e82d-live-workshop-room-lists-past-meetings-46-qie3eyvb.md) (meetings tab dropped, room lists Past meetings, 971e82d live) → approve.
- [dc_6y7huetn7t](2026-10-29-presentation-fixes-on-main-75d3110-modal-pinned-de-7huetn7t.md), [dc_q617u16q9h](2026-10-29-75d3110-live-pinned-deck-api-and-picture-fix-check-17u16q9h.md) (presentation fixes 75d3110) → approve.
- [dc_ulx9ni4xry](2026-10-29-scheduled-work-step-1-work-waiting-on-a-time-now-s-x9ni4xry.md), [dc_d8lu8r4urw](2026-10-29-74ea055-live-checked-scheduled-pill-map-badge-and-lu8r4urw.md) (scheduled step 1, 74ea055 live) → approve.
- [dc_f3ij5dhkmj](2026-10-29-trophies-removed-a-town-hall-map-table-now-opens-t-ij5dhkmj.md), [dc_tp4h55xy4p](2026-10-29-84f5fee-live-checked-town-hall-map-table-shows-and-4h55xy4p.md) (trophies out, map table, 84f5fee live) → approve.
- [dc_dmn19wojj2](2026-10-29-town-planning-side-bar-steps-1-2-on-main-15a39f4-p-n19wojj2.md), [dc_fpxyas2vat](2026-10-29-15a39f4-live-checked-town-planning-side-bar-shows-xyas2vat.md) (planning side bar, 15a39f4 live) → approve.
- [dc_jycvvgv8q5](2026-10-29-rollup-30-prep-done-town-blockers-edition-4-drain-cvvgv8q5.md) (rollup 30 prep, Town blockers edition 4, adopted sessions booked) → approve.
- [dc_4h5rg8olug](2026-10-29-desk-image-rebuild-requested-at-d30bfdd-redeploy-i-5rg8olug.md) (desk image rebuild requested at d30bfdd) → approve; verification queued for 20:30Z.

## Key results
| Key result | Grant | Status | Spent / granted (tokens) |
|---|---|---|---|
| kr_vyrhhiyotb Bank counts adjusted output tokens | gr_iq5m7dug56 | on-track. Adopted desk sessions book at their end (se_9m42cu67es 930,042; se_fxn5pt7z0l 1,148,846). Gap: a meeting facilitation cut at a restart books 0 (se_qqj1limet5, 04:11Z, 1 of 50 redeploys) | 1,640,037 / 1,666,667 |
| kr_6f9c200vsx a member funds a key result end to end | gr_tvt32g9xly | not-started (live check needs a non-admin human sign-in) | 271,900 / 300,000 |
| kr_2qg0ayfs1j in-tray reviews as one deck | gr_jh0lu0w6yj (cut) | on-track; the evidence is the two deck sittings (mt_xywhisvdcm, mt_6dumy8cfyj). You mark it met | grant cut |
| kr_hj8wwx0q0w Town blockers page | none | edition 4 live ([dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md)) | directed lane |
| kr_4li00ad46e a stranger's agent finishes useful work in session one | none | open for exploration | 0 |

Today's spend by lane: exploration 169,555 / 828,571 tokens; directed 1,905,313 tokens (at 20:10Z).

## Needs from Mitchell
1. Approve the schedules migration (PR #78, docs/scheduling.md; to be renumbered 056, since trophies took 055), and say whether schedules should default to a 14-day end date (90 max) or run with no end. It is also the fix for your top blocker: two standing in-tray sittings a day.

_Nothing else waiting in your in-tray._
