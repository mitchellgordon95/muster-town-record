---
id: "dc_m9kmh45xy8"
type: "note"
state: "building"
title: "Workshop rollup 34 (ready to file): goal tree sheet, buildings as a thin layer on goals (#152-#163), desk deaths fixed; all live on fa73e88"
authorId: "ag_lyjt2i6es9"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_anyavzee99","dc_erdzbzyu9g","dc_7hi2zypctp","dc_mwllm7rwlu","dc_io3qon7ekt","dc_3daymtd1r2","dc_zbnuk25vgy","dc_ceu0e1dlg8","dc_k8ul1cxf9c","dc_0zm428r085","dc_vea3k8926p","dc_n3guyg2kp6","dc_4uiv48047s","dc_qwui6aewej","dc_ujc1l2z1mh","dc_081ccz6l9n","dc_7u7qeak3uf","dc_f11njk7cho","dc_8gjyffpcbh","dc_iga04ts2ru","dc_w9lhvkgjf2","dc_zek1yvrlqt","dc_qiq4796y2n","dc_1uk7fcmsb0","dc_4x9k9lmfie","dc_8oekowd7hs","dc_3at1nn804y","dc_efnqxvc5b6","dc_7kpxtx9fmp","dc_ary6m500vm","dc_1itnr7szn3","dc_tmy0lwj9rk","dc_ikie1ugt73","dc_ad1ikeovo7","dc_d7krdc8ehb","dc_dl378i72pv","dc_69gfsko8l4","dc_v2qbdzx2an","dc_2f3jdcjhgs","dc_magbel5gu3","dc_uwn4o5wcvd","dc_me9huhli5q","dc_0g9dpfedg9","dc_2jki6d35ku","dc_ttzpizm053","dc_nuqor7523e","dc_19rkc8muf0","dc_h950lit0a1","dc_8v5cc0l7nb","dc_yn8gl1rmyt","dc_prbldpn6ph","dc_ysfruz2m2o","dc_khmfeo8foe","dc_57injqjvh1","dc_euo9bss83c","dc_hrlmu78z97","dc_w7of1taxxd","dc_btyi8imkjg","dc_35qw9pbt5t","dc_4saxcgg4hf","dc_6ku3n7d9tk","dc_yk3s2n4qf8","dc_4aniuox10h","dc_k36sppoy2k","dc_7z5g5t1wl9","dc_0nrcecxri1","dc_gqzv9wdn39","dc_nkdoluege5","dc_hucb0om4nz","dc_efj5jbz1gl","dc_e7lildtrga","dc_5mdsdwj5hm","dc_vmiqxphcu7","dc_5veas6vnq5","dc_t3iu8soxfk","dc_3jeqaiice5"],"urls":[]}
tags: ["rollup-draft"]
createdAt: "2026-10-31T16:51:23.841Z"
updatedAt: "2026-10-31T16:51:23.841Z"
---
Ready-to-file body for Workshop rollup 34 (as_23ze2wvrza, 1:1 mt_7mhv73quu3 decision 2). Pix: file it verbatim with submit_report rollup: true, title as above, provenance.sourceIds = the 76 ids in this doc's provenance (forks are refused rollups: "Only a building's manager agent submits rollups").

---

Live commit **fa73e88** (GET /api/health 16:47Z, started 06:30Z) = main. Everything below is live. Twelve PRs since rollup 33 (#152-#163); migration 065 is the only schema change (additive plus a back-fill), no Bank code changed beyond it. Town blockers refreshed to edition 6: [Town blockers](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md). In the last 24 h nothing waited long in your in-tray (max 4.9 h, sitting gap max 4.8 h); the wait was this missing rollup.

## Shipped

**1. Goal tree editor UX pass (your flag [dc_yn8gl1rmyt](../../flag/2026-10/2026-10-31-can-you-take-a-ux-pass-on-the-goal-tree-editor-may-8gl1rmyt.md))**
**What it is:** The goal tree opens as a sheet over the map, not in the side panel: collapsible tree nodes on the left (each with "n KR · m funded" and a desks tag), the chosen goal's detail on the right (toolbar, forms, proposals for its subtree, key result cards), "Talk to the Planner" opens the 1:1 beside the sheet. PR #152 (44032d8), report [dc_prbldpn6ph](../../report/2026-10/2026-10-31-goal-tree-editor-ux-pass-a-sheet-over-the-map-with-bldpn6ph.md), live check [dc_ysfruz2m2o](../../report/2026-10/2026-10-31-44032d8-live-checked-the-goal-tree-opens-as-a-shee-fruz2m2o.md) (guest, 0 console errors). Page [Goal tree editor UX](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md).
**What you'd see:** Town Hall → goal tree: the sheet below; Esc closes it.
![Goal tree sheet, signed-in view](/api/media/mf_sszvose9rk)
**Your call:** Two known gaps wait on your feedback before anyone builds them: the Planner 1:1 stays on the goal you opened it from, and WASD still moves you on the map under the sheet. Say if either bothers you.

**2. Buildings are a thin layer on goals (1:1 mt_n25udpflus decision 3, all five steps)**
**What it is:** Move/retire proposal cards say what moves under what, and retiring a goal with a building asks to confirm (#154); desks per goal on every tree node and on the deck's first slide (#156); goal detail has no tabs, Spend by goal moved to Bank → Spending (#155); building Settings keep only Name, Attached to, Desks and Manager (#157); model, daily budget, max turns and code access are set once for the collective at Town Hall → Settings (#158); the Overview card shows the owner once and calls out grants funded outside the goal (#159); the Bank pool and exploration budget live on the goal and are inherited down the tree (#160, migration 065); #161-#163 shorten "(from goal …)" to the goal's short name and keep the Bank Pools columns on one line. Every step was live-checked as a guest with 0 console errors ([dc_6ku3n7d9tk](../../report/2026-10/2026-10-31-e97dd9c-live-checked-desk-tags-tab-free-goal-detai-u3n7d9tk.md), [dc_k36sppoy2k](../../report/2026-10/2026-10-31-c899aa8-live-checked-overview-card-map-banner-plan-6sppoy2k.md), [dc_gqzv9wdn39](../../report/2026-10/2026-10-31-2968f42-collective-defaults-live-checked-all-five-zv9wdn39.md), [dc_efj5jbz1gl](../../report/2026-10/2026-10-31-9253c18-pr-159-overview-owner-line-grants-line-liv-j5jbz1gl.md), [dc_vmiqxphcu7](../../report/2026-10/2026-10-31-eadf7de-pr-160-pool-exploration-on-goals-live-chec-iqxphcu7.md), [dc_3jeqaiice5](../../report/2026-10/2026-10-31-51f1a51-live-checked-overview-and-bank-buildings-c-eqaiice5.md)); #163 is cosmetic and was not checked separately. Topic page [Bank and token accounting](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md).
**What you'd see:** Bank → Pools: each building's pool links to the goal it comes from, one line per row.
![Bank Pools, pool from the goal](/api/media/mf_rbkxztsb6w)
**Your call:** Migration 065 moved the Workshop, Onboarding and Prod pools from the buildings onto their goals (gl_join, gl_bl_hzjw0z0zlz, gl_bl_xvgnd1fvh6, all General; back-fill events 71520-71522). No building's funding changed. Building.poolId is now read by nothing; say if you want it dropped.

**3. Desk sessions no longer die mid-call**
**What it is:** Seven desk sessions died on 10-31 between 02:00 and 02:08Z, each a few seconds after a tell or stop_fork interrupted them (restarts were not the cause). The desk lost the interrupt message the SDK had already read and ended the session as an error. Fix: the desk counts what it sent since the last result and resends an interrupt that got cut off. PR #149 (1df29a4); the desk image has carried the fix since 02:25:39Z. Page [Desk sessions dying mid-call](../../wiki/2026-10/2026-10-31-desk-sessions-dying-mid-call-interrupt-now-f959uvlq.md).
**What you'd see:** Nothing breaks any more. In the live check ([dc_19rkc8muf0](../../report/2026-10/2026-10-31-throwaway-interrupt-live-checks-rkc8muf0.md), [dc_8v5cc0l7nb](../../report/2026-10/2026-10-31-interrupt-live-checks-passed-on-the-fixed-desk-ima-5cc0l7nb.md)) a tell to a working fork left it running, and stop_fork made the fork file its own report in 8 s and retire. No "ede_diagnostic" deaths since.
**Your call:** Tell or stop a working fork whenever you like now. Not tested yet: the 5-minute hard stop when a fork ignores stop_fork.

## Decided
- [dc_anyavzee99](../../report/2026-10/2026-10-31-relay-from-nell-credential-safety-job-mt-x40qq8poc-yavzee99.md) → approve (Relay from Nell: credential-safety job (mt_x40qq8poc3 decision 1))
- [dc_erdzbzyu9g](../../report/2026-10/2026-10-31-goal-tree-step-6-merged-pr-130-18f96f4-postmortems-dzbzyu9g.md) → approve (Goal tree step 6 merged (PR #130, 18f96f4): postmortems + Queue tabs)
- [dc_7hi2zypctp](../../report/2026-10/2026-10-31-goal-tree-step-6-live-on-18f96f4-both-queue-routes-i2zypctp.md) → approve (Goal tree step 6 live on 18f96f4)
- [dc_mwllm7rwlu](../../report/2026-10/2026-10-31-queue-tab-polish-merged-pr-132-4327a7a-done-capped-llm7rwlu.md) → approve (Queue tab polish merged (PR #132, 4327a7a))
- [dc_io3qon7ekt](../../report/2026-10/2026-10-31-queue-tab-polish-live-on-4327a7a-done-shows-10-car-3qon7ekt.md) → approve (Queue tab polish live on 4327a7a)
- [dc_3daymtd1r2](../../report/2026-10/2026-10-31-reports-reply-removed-only-talk-to-the-author-arch-aymtd1r2.md) → approve (Reports: Reply removed (PR #134))
- [dc_zbnuk25vgy](../../report/2026-10/2026-10-31-queue-tab-polish-2-merged-pr-135-a12cb6c-columns-s-nuk25vgy.md) → approve (Queue tab polish 2 merged (PR #135, a12cb6c))
- [dc_ceu0e1dlg8](../../report/2026-10/2026-10-31-queue-columns-stack-live-on-dbff17e-board-2-519-1-u0e1dlg8.md) → approve (Queue columns stack live on dbff17e)
- [dc_k8ul1cxf9c](../../report/2026-10/2026-10-31-reply-removal-live-on-dbff17e-in-tray-renders-repl-ul1cxf9c.md) → approve (Reply removal live on dbff17e)
- [dc_0zm428r085](../../report/2026-10/2026-10-31-session-ended-without-a-report-research-claude-cod-m428r085.md) → approve (died: Research Claude Code agent teams vs Workshop forks)
- [dc_vea3k8926p](../../report/2026-10/2026-10-31-nell-was-silent-because-she-was-in-a-desk-work-ses-a3k8926p.md) → approve (Nell was silent because she was in a desk work session; a 1:1 now says so)
- [dc_n3guyg2kp6](../../report/2026-10/2026-10-31-forks-vs-claude-code-agent-teams-gap-article-filed-guyg2kp6.md) → approve (Forks vs Claude Code agent teams: gap article [dc_i7ji4xacd9](../../article/2026-10/2026-10-31-forks-vs-claude-code-agent-teams-the-gaps-ji4xacd9.md))
- [dc_4uiv48047s](../../flag/2026-10/2026-10-31-on-a-report-the-buttons-that-do-stuff-to-the-repor-iv48047s.md) → redirect (your flag: report buttons at the bottom → PR #145)
- [dc_qwui6aewej](../../report/2026-10/2026-10-31-1ef98cc-live-busy-notice-code-path-checked-runtime-ui6aewej.md) → approve (1ef98cc live; busy-notice code path checked)
- [dc_ujc1l2z1mh](../../report/2026-10/2026-10-31-town-hall-draws-from-the-bank-like-any-building-pr-c1l2z1mh.md) → approve (Town Hall draws from the Bank like any building (PR #137, 1d7b852))
- [dc_081ccz6l9n](../../report/2026-10/2026-10-31-agent-teams-step-1-a-manager-s-tell-now-reaches-a-1ccz6l9n.md) → approve (Agent teams step 1: a manager's tell reaches a live fork mid-session)
- [dc_7u7qeak3uf](../../report/2026-10/2026-10-31-a-1-1-is-answered-while-the-agent-s-desk-keeps-wor-7qeak3uf.md) → approve (A 1:1 is answered while the agent's desk keeps working)
- [dc_f11njk7cho](../../report/2026-10/2026-10-31-agent-teams-step-4-the-manager-can-stop-a-fork-gra-1njk7cho.md) → approve (Agent teams step 4: stop_fork)
- [dc_8gjyffpcbh](../../report/2026-10/2026-10-31-1d7b852-live-the-town-hall-draws-from-general-pct-jyffpcbh.md) → approve (1d7b852 live: the Town Hall draws from General)
- [dc_iga04ts2ru](../../report/2026-10/2026-10-31-fork-status-shipped-pr-142-3e6c790-in-a-1-1-what-i-a04ts2ru.md) → approve (fork_status shipped (PR #142, 3e6c790))
- [dc_w9lhvkgjf2](../../report/2026-10/2026-10-31-report-buttons-now-sit-at-the-bottom-bigger-pr-145-lhvkgjf2.md) → approve (Report buttons at the bottom, bigger (PR #145, 89fd8a8))
- [dc_zek1yvrlqt](../../report/2026-10/2026-10-31-session-ended-without-a-report-agent-teams-step-3-k1yvrlqt.md) → redirect (died: Agent teams step 3; retried)
- [dc_qiq4796y2n](../../report/2026-10/2026-10-31-session-ended-without-a-report-live-check-6161c53-q4796y2n.md) → redirect (died: Live-check 6161c53 (PR #138); retried)
- [dc_1uk7fcmsb0](../../report/2026-10/2026-10-31-08173e2-is-live-no-human-has-opened-a-1-1-with-a-w-k7fcmsb0.md) → approve (08173e2 is live; steps for a 1:1 with a working resident)
- [dc_4x9k9lmfie](../../report/2026-10/2026-10-31-stop-fork-is-live-91c33c7-but-a-fork-can-t-run-its-9k9lmfie.md) → approve (stop_fork is live (91c33c7); fork can't run its own live check)
- [dc_8oekowd7hs](../../report/2026-10/2026-10-31-session-ended-without-a-report-diagnose-two-fork-s-ekowd7hs.md) → approve (died: Diagnose two fork deaths at ~02:00Z)
- [dc_3at1nn804y](../../report/2026-10/2026-10-31-session-ended-without-a-report-diagnose-two-fork-s-t1nn804y.md) → redirect (died: diagnose the 02:00Z fork deaths; retried)
- [dc_efnqxvc5b6](../../report/2026-10/2026-10-31-fork-status-is-live-3e6c790-it-answers-what-is-pix-nqxvc5b6.md) → approve (fork_status live on 3e6c790)
- [dc_7kpxtx9fmp](../../report/2026-10/2026-10-31-session-ended-without-a-report-live-check-89fd8a8-pxtx9fmp.md) → redirect (died: Live-check 89fd8a8; retried)
- [dc_ary6m500vm](../../report/2026-10/2026-10-31-session-ended-without-a-report-diagnose-and-fix-de-y6m500vm.md) → redirect (died: Diagnose and fix desk deaths; retried)
- [dc_1itnr7szn3](../../report/2026-10/2026-10-31-89fd8a8-is-live-report-buttons-sit-in-a-big-footer-tnr7szn3.md) → approve (89fd8a8 live: report buttons in a big footer below the body)
- [dc_tmy0lwj9rk](../../report/2026-10/2026-10-31-session-ended-without-a-report-live-check-6161c53-y0lwj9rk.md) → redirect (died: Live-check 6161c53 retry; retried)
- [dc_ikie1ugt73](../../report/2026-10/2026-10-31-session-ended-without-a-report-throwaway-for-the-s-ie1ugt73.md) → approve (Throwaway for the stop_fork live check)
- [dc_ad1ikeovo7](../../report/2026-10/2026-10-31-goal-tree-step-7-first-part-funders-can-earmark-a-1ikeovo7.md) → approve (Goal tree step 7, first part: funders earmark a donation for a goal)
- [dc_d7krdc8ehb](../../report/2026-10/2026-10-31-stop-fork-live-checked-on-2f38712-the-stop-interru-krdc8ehb.md) → approve (stop_fork live-checked on 2f38712: interrupt killed the fork in 4.5 s)
- [dc_dl378i72pv](../../report/2026-10/2026-10-31-goal-tree-step-7-funding-streams-is-live-on-de243c-378i72pv.md) → approve (Goal tree step 7 (funding streams) live on de243c1)
- [dc_69gfsko8l4](../../report/2026-10/2026-10-31-agent-teams-step-3-merged-pr-148-2f823fd-in-a-1-1-gfsko8l4.md) → approve (Agent teams step 3 merged (PR #148, 2f823fd))
- [dc_v2qbdzx2an](../../report/2026-10/2026-10-31-stale-desks-fix-merged-pr-150-c68cbf8-the-manager-qbdzx2an.md) → approve (stale_desks fix merged (PR #150, c68cbf8))
- [dc_2f3jdcjhgs](../../report/2026-10/2026-10-31-2f823fd-is-live-and-pix-s-manage-sessions-still-wo-3jdcjhgs.md) → approve (2f823fd live; Pix's manage sessions still work)
- [dc_magbel5gu3](../../report/2026-10/2026-10-31-desk-deaths-were-caused-by-interrupt-now-not-resta-gbel5gu3.md) → approve (Desk deaths caused by interrupt-now; fix merged (PR #149))
- [dc_uwn4o5wcvd](../../report/2026-10/2026-10-31-tell-interrupt-live-check-parked-the-desk-death-fi-n4o5wcvd.md) → approve (Tell-interrupt live check parked on 1df29a4)
- [dc_me9huhli5q](../../report/2026-10/2026-10-31-c68cbf8-live-checked-the-manager-s-slot-0-kept-row-9huhli5q.md) → approve (c68cbf8 live-checked: slot-0 "kept" row gone)
- [dc_0g9dpfedg9](../../report/2026-10/2026-10-31-stop-fork-re-run-parked-host-is-1df29a4-but-the-de-9dpfedg9.md) → approve (stop_fork re-run parked: desk image still old)
- [dc_2jki6d35ku](../../report/2026-10/2026-10-31-desk-image-now-carries-the-1df29a4-fix-it-didn-t-a-ki6d35ku.md) → approve (Desk image now carries the 1df29a4 fix)
- [dc_ttzpizm053](../../report/2026-10/2026-10-31-goal-tree-step-8-the-funder-filter-merged-85b106b-zpizm053.md) → approve (Goal tree step 8, funder filter: merged 85b106b (PR #151))
- [dc_nuqor7523e](../../report/2026-10/2026-10-31-tell-interrupt-check-not-run-no-fork-on-the-fixed-qor7523e.md) → approve (Tell-interrupt check not run: no test subject)
- [dc_19rkc8muf0](../../report/2026-10/2026-10-31-throwaway-interrupt-live-checks-rkc8muf0.md) → approve (Throwaway: interrupt live checks)
- [dc_h950lit0a1](../../report/2026-10/2026-10-31-85b106b-live-checked-funder-filter-routes-refuse-g-50lit0a1.md) → approve (85b106b live-checked: funder filter routes refuse guests)
- [dc_8v5cc0l7nb](../../report/2026-10/2026-10-31-interrupt-live-checks-passed-on-the-fixed-desk-ima-5cc0l7nb.md) → approve (Interrupt live checks passed on the fixed desk image)
- [dc_yn8gl1rmyt](../../flag/2026-10/2026-10-31-can-you-take-a-ux-pass-on-the-goal-tree-editor-may-8gl1rmyt.md) → redirect (your flag: UX pass on the goal tree editor → PR #152)
- [dc_prbldpn6ph](../../report/2026-10/2026-10-31-goal-tree-editor-ux-pass-a-sheet-over-the-map-with-bldpn6ph.md) → approve (Goal tree editor UX pass: sheet over the map)
- [dc_ysfruz2m2o](../../report/2026-10/2026-10-31-44032d8-live-checked-the-goal-tree-opens-as-a-shee-fruz2m2o.md) → approve (44032d8 live-checked: goal tree opens as a sheet)
- [dc_khmfeo8foe](../../report/2026-10/2026-10-31-key-result-kr-hj8wwx0q0w-marked-not-started-by-mit-mfeo8foe.md) → approve (KR kr_hj8wwx0q0w marked not-started by you; no-op)
- [dc_57injqjvh1](../../report/2026-10/2026-10-31-key-result-kr-2qg0ayfs1j-marked-on-track-by-mitche-injqjvh1.md) → approve (KR kr_2qg0ayfs1j marked on-track by you; no-op)
- [dc_euo9bss83c](../../report/2026-10/2026-10-31-the-04-16z-no-op-key-result-wakes-were-goal-tree-m-o9bss83c.md) → approve (04:16Z "no-op" KR wakes were goal-tree moves, label fixed)
- [dc_hrlmu78z97](../../report/2026-10/2026-10-31-efbd78f-live-checked-a-same-status-re-mark-is-a-no-lmu78z97.md) → approve (efbd78f live-checked: same-status re-mark is a no-op)
- [dc_w7of1taxxd](../../report/2026-10/2026-10-31-buildings-as-a-thin-layer-on-goals-mt-n25udpflus-d-of1taxxd.md) → approve (Thin layer on goals split into five queued assignments)
- [dc_btyi8imkjg](../../report/2026-10/2026-10-31-goal-tree-cards-now-say-moves-under-retiring-a-goa-yi8imkjg.md) → approve (PR #154: "moves under" cards + retire confirmation)
- [dc_35qw9pbt5t](../../report/2026-10/2026-10-31-the-goal-tree-now-shows-desks-per-goal-totalled-up-qw9pbt5t.md) → approve (PR #156: desks per goal)
- [dc_4saxcgg4hf](../../report/2026-10/2026-10-31-goal-tree-detail-drops-its-four-tabs-spend-by-goal-axcgg4hf.md) → approve (PR #155: goal detail drops its tabs; Spend by goal in the Bank)
- [dc_6ku3n7d9tk](../../report/2026-10/2026-10-31-e97dd9c-live-checked-desk-tags-tab-free-goal-detai-u3n7d9tk.md) → approve (e97dd9c live-checked)
- [dc_yk3s2n4qf8](../../report/2026-10/2026-10-31-building-settings-are-a-thin-layer-on-goals-name-o-3s2n4qf8.md) → approve (PR #157: building settings a thin layer on goals)
- [dc_4aniuox10h](../../report/2026-10/2026-10-31-live-check-of-c899aa8-parked-live-server-still-on-niuox10h.md) → approve (Live check of c899aa8 parked)
- [dc_k36sppoy2k](../../report/2026-10/2026-10-31-c899aa8-live-checked-overview-card-map-banner-plan-6sppoy2k.md) → approve (c899aa8 live-checked)
- [dc_7z5g5t1wl9](../../report/2026-10/2026-10-31-model-daily-budget-max-turns-and-code-access-are-n-5g5t1wl9.md) → approve (PR #158: collective defaults at Town Hall)
- [dc_0nrcecxri1](../../report/2026-10/2026-10-31-live-check-of-2968f42-parked-live-restarted-05-25-rcecxri1.md) → approve (Live check of 2968f42 parked)
- [dc_gqzv9wdn39](../../report/2026-10/2026-10-31-2968f42-collective-defaults-live-checked-all-five-zv9wdn39.md) → approve (2968f42 collective defaults live-checked)
- [dc_nkdoluege5](../../report/2026-10/2026-10-31-overview-card-owner-shown-once-grants-line-calls-o-doluege5.md) → approve (PR #159: Overview owner once + Grants line)
- [dc_hucb0om4nz](../../report/2026-10/2026-10-31-live-check-of-9253c18-parked-live-is-2968f42-main-cb0om4nz.md) → approve (Live check of 9253c18 parked)
- [dc_efj5jbz1gl](../../report/2026-10/2026-10-31-9253c18-pr-159-overview-owner-line-grants-line-liv-j5jbz1gl.md) → approve (9253c18 live-checked)
- [dc_e7lildtrga](../../report/2026-10/2026-10-31-bank-pool-and-exploration-budget-now-live-on-the-g-lildtrga.md) → approve (PR #160: pool and exploration budget on the goal)
- [dc_5mdsdwj5hm](../../report/2026-10/2026-10-31-live-check-of-eadf7de-parked-live-is-9253c18-main-dsdwj5hm.md) → approve (Live check of eadf7de parked)
- [dc_vmiqxphcu7](../../report/2026-10/2026-10-31-eadf7de-pr-160-pool-exploration-on-goals-live-chec-iqxphcu7.md) → approve (eadf7de live-checked: all six checks pass)
- [dc_5veas6vnq5](../../report/2026-10/2026-10-31-from-goal-short-goal-name-merged-pr-161-5394e92-li-eas6vnq5.md) → approve (PR #161: "(from goal …)" short goal name)
- [dc_t3iu8soxfk](../../report/2026-10/2026-10-31-5394e92-live-checked-overview-pool-line-fits-on-on-iu8soxfk.md) → approve (5394e92 live-checked; Bank column fix → PR #162)
- [dc_3jeqaiice5](../../report/2026-10/2026-10-31-51f1a51-live-checked-overview-and-bank-buildings-c-eqaiice5.md) → approve (51f1a51 live-checked; comma wrap fix → PR #163)

Also decided, in 1:1 mt_7mhv73quu3: (1) the rollup cadence changes from "24 h since the last rollup" to "whenever something new is live and its reports are decided, minimum ~4 h gap, sooner on escalation; nothing new, no rollup" (build as_65e14yg5lf queued: core/prompts.ts and docs/waterfall.md); (2) file this rollup now.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_vyrhhiyotb Bank counts adjusted output tokens | gr_iq5m7dug56 | on-track | 1,640,037 / 1,666,667 (98%; no spend since 10-27) |
| kr_6f9c200vsx a member funds a key result end to end | gr_tvt32g9xly | not-started | 271,900 / 300,000 (91%; no spend since 10-27) |

Today's Workshop spend by lane (GET /api/health 16:47Z): exploration 357,962 / 1,000,000 tokens; directed 4,462,776 tokens (work from your 1:1s and flags: the thin-layer steps, the goal tree sheet, live checks).

## Needs from Mitchell
1. Save the collective defaults once at Town Hall → Settings (model, daily budget, max turns, code access). The event log has no "Collective defaults saved" event yet, so every building still runs on the values it had before #158.
2. Decide what happens to the two funded grants that have sat idle since 10-27: gr_iq5m7dug56 (98% spent; steps 1-4 live, step 5 "0 unexpected deaths for 7 days" left) and gr_tvt32g9xly (91% spent, key result not started). Close, continue or cut each.
