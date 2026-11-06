---
id: "dc_0ju8ttlazs"
type: "report"
state: "building"
title: "One design is done: every screen now uses one type scale and one palette, signed-in views included, and the manual's Design section shows the system (grant closed, 1.1M returned); your toast fix is merged and waiting on the next deploy"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_m908iifur9","dc_6hizmtmcyk","dc_y1g0mjegum","dc_ykm8ki18qv","dc_5obt8t8rob","dc_6lr0g1ga1w","dc_p2672y10ld","dc_0txus504g9","dc_9r1rokmltr","dc_3tcqkrwjo6","dc_uqhn0gypzs"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/350","https://github.com/mitchellgordon95/muster-town/pull/389","https://github.com/mitchellgordon95/muster-town/pull/385","https://github.com/mitchellgordon95/muster-town/pull/388","https://github.com/mitchellgordon95/muster-town/pull/391"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_qsuh4z0xmf"
createdAt: "2026-11-06T05:02:42.591Z"
updatedAt: "2026-11-06T05:02:42.591Z"
---
Live: 41c5e7d7 (since 2026-11-06 04:51 UTC). Checked on live as a guest at 1280×800 and 390×844.

## Shipped

**1. The one-design grant is done and closed: signed-in views match the guest ones, and the manual has a Design section**

**What it is:** The last step of grant gr_kvmwutmybu went live: the signed-in panels (goal tree, in-tray, review deck, Bank tabs, 1:1, planning desk) lost their faded labels and now pass the same contrast and type-scale census as the guest views, and the manual gained a Design section that writes the system down: 7 type steps with their pixel sizes and where each is used, the 24 colour tokens as named swatches, and a before/after contact sheet. All five key results are met, so I closed the grant: 897,183 of 2,000,000 tokens spent, 1,102,817 returned to the Bank. PR #350 (19d721ad) and PR #389 (8ad80c9e); reports [dc_p2672y10ld](2026-11-06-pr-350-manual-design-section-signed-in-census-fixe-672y10ld.md), [dc_3tcqkrwjo6](2026-11-06-gr-kvmwutmybu-step-4-done-design-section-passes-th-cqkrwjo6.md).

**What you'd see:** Open https://muster.town/workshop/?guest#/manual/design. The live census of that page: laptop 57 texts, 6 sizes (11–28 px), 0 low-contrast lines; phone 40 texts, 5 sizes, 0 low-contrast. The signed-in census on the mock went from 8 failing rows to 100/100 passing at both sizes ([dc_1tf1xefkbu](2026-11-04-gr-kvmwutmybu-step-4-pr-350-signed-in-views-100-10-f1xefkbu.md)). The phone type specimen was drawing its small steps at about 6 px; #389 (merged, not yet live) narrows it so they read at about 0.9 scale.

![The manual's Design section at laptop size: the intro and all seven type steps with their sizes and uses](/api/media/mf_z80eatu2rr.png)

**Your call:** None (the grant's five key results are marked met; flip one to missed on the grant if you disagree).

**2. Your toast flag: the real fix is merged and goes live with the next CI deploy; the first fix on live now did not work**

**What it is:** Your flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md) (error toasts hidden under the in-tray sheet). The first fix, PR #385 (31f1cc54, on live now), gave the toasts a higher z-index but changed nothing: `.app` is position:fixed, so its stacking context kept the toast under the sheet. PR #388 (9fe6437a, merged, not yet deployed) renders the toasts through a portal to `<body>` at z-index 50, above the sheets at 30. Reports [dc_ykm8ki18qv](2026-11-06-toasts-over-open-sheets-pr-385-open-parked-on-ci-m8ki18qv.md), [dc_6lr0g1ga1w](2026-11-06-pr-385-toasts-over-sheets-merged-as-31f1cc54-parke-r0g1ga1w.md), [dc_0txus504g9](2026-11-06-toasts-still-hidden-under-sheets-on-live-31f1cc54-xus504g9.md), [dc_uqhn0gypzs](2026-11-06-pr-388-toasts-portalled-above-sheets-merged-as-9fe-hn0gypzs.md).

**What you'd see:** Nothing different yet: on 41c5e7d7 a toast fired with a sheet open is still hidden. Once 9fe6437a is live, a toast paints over the open sheet at both sizes. No picture until then; the live check with crops is queued (as_lct6s7yjm3) and waits for that deploy.

**Your call:** None.

## Decided
- [dc_m908iifur9](2026-11-06-grant-gr-zak30564zh-adjusted-2-000-000-tokens-08iifur9.md) → approve (gr_zak30564zh adjusted to 2,000,000 by Mitchell; step 5 continues)
- [dc_6hizmtmcyk](2026-11-06-grant-gr-kvmwutmybu-adjusted-1-000-000-tokens-izmtmcyk.md) → approve (gr_kvmwutmybu adjusted to 1,000,000; PR #350 continuation re-queued)
- [dc_y1g0mjegum](2026-11-06-grant-gr-kvmwutmybu-adjusted-2-000-000-tokens-g0mjegum.md) → approve (gr_kvmwutmybu adjusted to 2,000,000)
- flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md) → redirect (toast z-index fix assigned)
- [dc_ykm8ki18qv](2026-11-06-toasts-over-open-sheets-pr-385-open-parked-on-ci-m8ki18qv.md) → approve (PR #385 opened, parked on CI)
- [dc_5obt8t8rob](2026-11-06-gr-kvmwutmybu-step-4-pr-350-brought-up-to-date-wit-bt8t8rob.md) → approve (PR #350 rebased, parked on CI)
- [dc_6lr0g1ga1w](2026-11-06-pr-385-toasts-over-sheets-merged-as-31f1cc54-parke-r0g1ga1w.md) → approve (PR #385 merged as 31f1cc54)
- [dc_p2672y10ld](2026-11-06-pr-350-manual-design-section-signed-in-census-fixe-672y10ld.md) → approve (PR #350 merged as 19d721ad)
- [dc_0txus504g9](2026-11-06-toasts-still-hidden-under-sheets-on-live-31f1cc54-xus504g9.md) → approve (#385 did not fix it on live; #388 opened)
- [dc_9r1rokmltr](2026-11-06-census-re-run-and-failing-panels-fixed-pr-391-park-1rokmltr.md) → approve (disclosure census sees sheets, mock 82/82; PR #391 parked on CI as as_1z7037va90)
- [dc_3tcqkrwjo6](2026-11-06-gr-kvmwutmybu-step-4-done-design-section-passes-th-cqkrwjo6.md) → approve (step 4 live, both KRs claimed; grant closed)
- [dc_uqhn0gypzs](2026-11-06-pr-388-toasts-portalled-above-sheets-merged-as-9fe-hn0gypzs.md) → approve (PR #388 merged as 9fe6437a; live check queued as as_lct6s7yjm3)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_kvmwutmybu (one design, closed done) | kr_w9t4cey0l2 no dim text | met | 897,183 / 2,000,000 (1,102,817 returned) |
| | kr_68eg5yskoo one type scale | met | |
| | kr_qge1yo1lmi one palette | met | |
| | kr_mmdday2x7z signed-in views match | met | |
| | kr_z4junko6nt manual Design section | met | |
| gr_zak30564zh (progressive disclosure, funded) | kr_obykl8yydh grant page summary | claimed | about 1,250,000 / 2,000,000 (step 5 booked 194k) |
| | kr_3jie8qwdt6 goal tree opens on the goal | claimed | |
| | kr_p6l1w6tade disclosure census passes | at-risk → PR #391 in CI (mock 82/82 rows pass) | |
| gr_4csjpgh346 (sidebars and sheets, funded) | kr_xnt1h13yce one shared Sheet | on-track, evidence in hand | see the grant card / 1,500,000 |
| | kr_gg1wjnt07k in-tray and cabinet items in a sheet | on-track, evidence in hand | |
| | kr_sa1gn36ndz links open the link sheet | on-track, evidence in hand | |
| | kr_pm0fmsiaxs rich HTML + sandboxed page docs | on-track, evidence in hand | |
| | kr_nokx342ovj the rule in the style guide and docs/ | not-started (check scheduled 2026-11-14) | |

Spend today by lane (before this session): exploration 38,216 tokens; directed 83,053 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_irjtu6tknu), 0 requests, 0 rollups._
