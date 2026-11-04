---
id: "dc_5f1np62hlp"
type: "report"
state: "building"
title: "Rollup 47: Daily digest button and grouped digest card live, in-tray Cards view removed, hosted collectives name their own captain (aa6f4fbc)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_yp9ofcnhny","dc_95bf6fxa4g","dc_odbjvpoh9l","dc_oncz7su0tv","dc_9c2dgw7kp6","dc_hrmbvc4ohw","dc_xmqqnr4nrc","dc_4w5e5uvsw4","dc_ycocv32ibe","dc_uekq0ag533","dc_l77dl3bwph","dc_ualrq1pnzl","dc_jcs6svrnmt","dc_gxtxualbsp","dc_hrptju2s61","dc_6yjf5orfta","dc_rju0tw41ou","dc_58bp6zln1c","dc_h2dpn933pb","dc_o7mbgxpdvc","dc_gzw9ibc73a","dc_otlpmgjxn1","dc_0m1p6kk54q","dc_3zmyrznhud","dc_1zlq030i4m"],"urls":["https://muster.town/api/health","https://github.com/mitchellgordon95/muster-town/pull/346","https://github.com/mitchellgordon95/muster-town/pull/337","https://github.com/mitchellgordon95/muster-town/pull/347"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_ozpbmoj44s"
createdAt: "2026-11-04T23:08:33.071Z"
updatedAt: "2026-11-04T23:08:33.071Z"
---
Live: aa6f4fbc since 20:40 UTC (health read by Pix 1 at 23:05:10Z); every change below is an ancestor of it.

## Shipped

**1. A "Daily digest" button and a grouped digest card in the Town Hall in-tray**
**What it is:** The Secretary's digest card now groups "Decisions needed" into Money, Go / no-go, Questions in words, Already overtaken (with one "Approve all" button) and Errands, and groups "Shipped" by theme. A "Daily digest" button next to "Talk to Secretary" runs the digest on demand for you; guests get no button and the run route refuses them. The in-tray crash you flagged is fixed. PRs #317, #345, #346, #328; reports [dc_95bf6fxa4g](2026-11-04-daily-digest-button-346-is-live-on-aa6f4fbc-guests-bf6fxa4g.md), [dc_odbjvpoh9l](2026-11-04-secretary-step-3e-is-live-on-b55ecf9c-the-digest-s-bjvpoh9l.md), [dc_hrptju2s61](2026-11-04-in-tray-crash-fixed-live-bcec74f-list-cards-stoppe-ptju2s61.md).
**What you'd see:** Town Hall in-tray header: ▶ Review as deck, Talk to Secretary, Daily digest. The digest card at the top shows "Decisions needed › Money (10)" live; the next scheduled card lands at 07:00 UTC (about 8 h from now) on the funded retainer.
![Guest view of the Town Hall in-tray: header with Review as deck and the Secretary's grouped digest card](/api/media/mf_itjijx3uda.png)
**Your call:** Press "Daily digest" now to get today's grouped card, or wait for the 07:00 UTC fire; either way, tell me if the groups read wrong.

**2. The in-tray's Cards view is gone**
**What it is:** The List / Cards toggle and the big-card view were removed from the Town Hall in-tray and building in-trays, as you asked in the 1:1 (mt_i50xwu4z2t). One compact list with click-to-open, plus the review deck. PR #337 = 17d00eb; reports [dc_ualrq1pnzl](2026-11-04-in-tray-cards-view-removed-for-everyone-pr-337-ope-lrq1pnzl.md), [dc_ycocv32ibe](2026-11-04-pr-337-in-tray-cards-view-removed-merged-as-17d00e-ocv32ibe.md).
**What you'd see:** The picture above: the only mode button is "▶ Review as deck"; no toggle anywhere. Pix 1's page scan found 22 in-tray lines, 21 waiting, no crash.
**Your call:** None.

**3. Hosted collectives name their own captain; repo-less collectives hide the deploy machinery**
**What it is:** Prompts, the checkpoint kickoff and the rollup heading now say "Needs from <root captain>" in a hosted collective ("Needs from Ada"), falling back to the first admin; muster.town comes out byte-identical ("Needs from Mitchell", checked live). Collectives with no repo get no "Pull main & redeploy" and no `redeploy` tool. PRs #347 = c7ae8169 and #333 = 4815e19; reports [dc_hrmbvc4ohw](2026-11-04-hosted-collectives-prompts-and-rollup-heading-name-mbvc4ohw.md), [dc_oncz7su0tv](2026-11-04-c7ae8169-hosted-collectives-name-their-captain-is-cz7su0tv.md), [dc_xmqqnr4nrc](2026-11-04-pr-333-repo-mode-hides-deploy-pr-machinery-from-re-qqnr4nrc.md). Prompt and API only: nothing changes in muster.town's UI.
**What you'd see:** Nothing new here; on a hosted /<slug>/ the Planning → System page has no redeploy button and its managers' rollups carry the captain's name.
**Your call:** None.

## Decided
- [dc_yp9ofcnhny](2026-11-04-rollup-47-materials-all-four-changes-are-live-on-a-9ofcnhny.md) → approve (rollup 47 materials: all four shas live, picture, grant figures)
- [dc_95bf6fxa4g](2026-11-04-daily-digest-button-346-is-live-on-aa6f4fbc-guests-bf6fxa4g.md) → approve (#346 live; guest gets no button, run route → 401)
- [dc_odbjvpoh9l](2026-11-04-secretary-step-3e-is-live-on-b55ecf9c-the-digest-s-bjvpoh9l.md) → approve (3e live on b55ecf9c; groups read right)
- [dc_oncz7su0tv](2026-11-04-c7ae8169-hosted-collectives-name-their-captain-is-cz7su0tv.md) → approve (#347 live; muster.town unchanged; two text leftovers not worth a session)
- [dc_9c2dgw7kp6](2026-11-04-pr-347-hosted-collectives-name-their-captain-merge-2dgw7kp6.md) → approve (#347 merged as c7ae8169, parked on the deploy)
- [dc_hrmbvc4ohw](2026-11-04-hosted-collectives-prompts-and-rollup-heading-name-mbvc4ohw.md) → approve (#347 captainName(), parked on CI)
- [dc_xmqqnr4nrc](2026-11-04-pr-333-repo-mode-hides-deploy-pr-machinery-from-re-qqnr4nrc.md) → approve (#333 merged as 4815e19; live check queued separately)
- [dc_4w5e5uvsw4](2026-11-04-pr-333-conflicted-with-main-again-after-green-ci-r-5e5uvsw4.md) → approve (#333 conflict resolved, parked on CI)
- [dc_ycocv32ibe](2026-11-04-pr-337-in-tray-cards-view-removed-merged-as-17d00e-ocv32ibe.md) → approve (#337 merged as 17d00eb)
- [dc_uekq0ag533](2026-11-04-pr-337-conflicted-with-main-again-manual-md-merged-kq0ag533.md) → approve (#337 manual.md conflict, parked on CI)
- [dc_l77dl3bwph](2026-11-04-pr-337-merged-with-main-after-328-landed-parked-on-7dl3bwph.md) → approve (#337 rebased after #328)
- [dc_ualrq1pnzl](2026-11-04-in-tray-cards-view-removed-for-everyone-pr-337-ope-lrq1pnzl.md) → approve (#337 opened)
- [dc_jcs6svrnmt](2026-11-04-pr-346-conflicted-with-main-cards-view-removal-mer-s6svrnmt.md) → approve (#346 rebased after #337)
- [dc_gxtxualbsp](2026-11-04-session-ended-without-a-report-a-daily-digest-butt-txualbsp.md) → redirect (Pix 3's digest-button session died in a background check; recovered as #346)
- [dc_hrptju2s61](2026-11-04-in-tray-crash-fixed-live-bcec74f-list-cards-stoppe-ptju2s61.md) → approve (your in-tray crash flag [dc_zeguj4r2po](../../flag/2026-11/2026-11-04-town-intray-is-currently-crashing-with-guj4r2po.md) fixed live in bcec74f)
- [dc_6yjf5orfta](2026-11-04-pr-336-a-continue-adjust-cut-cancels-a-stale-write-jf5orfta.md) → approve (#336 merged as c46e07b: a continue/adjust/cut cancels a stale checkpoint assignment)
- [dc_rju0tw41ou](2026-11-04-checkpoint-for-gr-kdlogzzo5s-overtaken-mitchell-ad-u0tw41ou.md) → approve (checkpoint overtaken by your adjust; statuses set on the grant)
- [dc_58bp6zln1c](2026-11-04-pr-317-grouped-digest-card-green-and-merged-as-d15-bp6zln1c.md), [dc_h2dpn933pb](2026-11-04-pr-317-had-no-ci-run-on-b21f794-it-conflicted-with-dpn933pb.md), [dc_o7mbgxpdvc](2026-11-04-pr-317-failed-ci-only-on-the-dead-code-check-unuse-mbgxpdvc.md), [dc_otlpmgjxn1](2026-11-04-digest-card-clustered-both-sections-and-overtaken-lpmgjxn1.md) → approve (#317 grouped card: built, two conflict rounds, merged as d156a72)
- [dc_gzw9ibc73a](2026-11-04-grant-gr-kdlogzzo5s-adjusted-1-500-000-tokens-w9ibc73a.md) → approve (you adjusted gr_kdlogzzo5s to 1,500,000 at 18:27Z)
- [dc_0m1p6kk54q](2026-11-04-secretary-step-3b-talk-to-secretary-everywhere-tow-1p6kk54q.md) → approve (#308 Talk to Secretary everywhere; Town Hall manager row = root captain)
- [dc_3zmyrznhud](2026-11-04-90212da-live-in-tray-carries-digest-retainer-appro-myrznhud.md), [dc_1zlq030i4m](2026-11-04-pr-305-secretary-step-3-merged-as-90212da-redeploy-lq030i4m.md) → approve (#305 live; retainer sc_8zoclbtrwp funded 140,000, first fire 07:00Z 11-05)
- From Prod (Cleo 1, ms_imo0kxsvbr): your backup ask from mt_1vs893enaw is live in #316 (hosted DBs and transcripts hourly); it is in Prod's rollup, not ours.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_kdlogzzo5s Secretary | kr_spolcs3akx digest card first in the in-tray | on-track (card live; first scheduled card 07:00Z 11-05) | 1,259,525 / 1,500,000 |
| gr_kdlogzzo5s | kr_rl8l0xfrkm approved daily retainer on the Secretary | on-track (sc_8zoclbtrwp funded 140,000, 0 runs) | " |
| gr_kdlogzzo5s | kr_nt0q4a3pmy a 1:1 decision applied via the Secretary | on-track (code live; no real decision yet) | " |
| gr_kdlogzzo5s | kr_sdtzgbyrxn core and server tests | claimed | " |

Spend today by lane: exploration 72,681 tokens; directed 2,517,694 tokens. Scheduled: step 4a check at 07:30Z 11-05 (did the first digest fire), onboarding staleness sweep daily 19:00Z.

## Needs from Mitchell
- Open "Talk to Secretary" once and say one decision in your own words (e.g. "approve that retainer" or "continue gr_x at 200k"): that gives kr_nt0q4a3pmy its first real record on a grant's history, which only you can produce.

_Already waiting in your in-tray: 1 proposal (gr_cwwtrabt2o), 2 requests ([dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md), [dc_wawcjkger2](../../../../../town-hall/outbox/2026-11/2026-11-04-publish-to-github-live-check-an-empty-github-repo-wcjkger2.md)), 1 rollup ([dc_cz38wq3sq4](2026-11-04-close-rollup-gr-8i952perny-stopping-a-funded-grant-38wq3sq4.md))._
