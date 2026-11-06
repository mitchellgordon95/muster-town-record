---
id: "dc_kopnqv6zhz"
type: "report"
state: "building"
title: "Progressive disclosure is done: every grant page, building tab and agent tab opens on a short first screen (grant closed, 730k returned); your toast fix is live"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_k0lx8h2hwa","dc_mow5mjh10x","dc_0gcm0c3lhh"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/391","https://github.com/mitchellgordon95/muster-town/pull/388","https://github.com/mitchellgordon95/muster-town/pull/389"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-06T17:16:21.305Z"
sessionId: "se_g00xwoficn"
createdAt: "2026-11-06T05:31:23.066Z"
updatedAt: "2026-11-06T17:16:21.305Z"
---
Live: 24984fc6 (since 2026-11-06 05:21 UTC). Filed 30 min after the last rollup rather than 4 h because a grant closed. Checked on live as a guest at 1280×800 and 390×844.

## Shipped

**1. The progressive-disclosure grant is done and closed: grant pages, building tabs and agent tabs open on a summary, and a census proves it**

**What it is:** The last step of grant gr_zak30564zh went live with PR #391 (24984fc6). A repeatable disclosure census now opens every panel and tab as a guest at laptop and phone size and counts controls and words on the first screen; the panels that failed (grant pages, building Goals/Grants/Queue tabs, agent tabs) got folds so the detail is one click away. All three key results are claimed on live, so I closed the grant: 1,269,664 of 2,000,000 tokens spent, 730,336 returned to the Bank. Reports [dc_0gcm0c3lhh](2026-11-06-kr-p6l1w6tade-on-live-24984fc6-all-70-counted-rows-cm0c3lhh.md), [dc_9r1rokmltr](2026-11-06-census-re-run-and-failing-panels-fixed-pr-391-park-1rokmltr.md), [dc_k0lx8h2hwa](2026-11-06-pr-391-disclosure-census-panel-folds-merged-as-249-lx8h2hwa.md).

**What you'd see:** Open https://muster.town/workshop/?guest and the grant gr_zak30564zh: its first screen has 10 controls and 161 words (was 358 words), each key result one line with a "details" fold, Plan/Sessions/History folded. The live census: 70 of 70 counted rows pass the bar (≤12 controls, ≤200 words on the first screen) at both sizes, across 5 grants, 4 buildings × 5 tabs, 2 agents, a meeting, the goal-tree detail and connect; the signed-in admin mock passes 82/82. Excluded by design: the Bank, document bodies, the goal-tree canvas. Building Goals tabs still run 3–7 screens in total, but their first screens pass.

![Grant gr_zak30564zh's first screen on live: a summary with each key result on one line and a details fold](/api/media/mf_calgbffitb.png)

**Your call:** None (the three key results are marked met; flip one to missed on the grant if you disagree).

**2. Your toast flag is fixed on live: error toasts now paint over an open sheet at both sizes**

**What it is:** Your flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md) (error toasts hidden under the in-tray sheet). PR #388 (9fe6437a) renders toasts through a portal to `<body>` above the sheets; it went live with 24984fc6. Teo 2 opened a doc sheet from the Town Hall in-tray, fired a toast and checked what sits at the toast's centre: the toast itself, at 1280×800 and 390×844. The phone type specimen in the manual's Design section (#389) now draws its small steps at about 10 px instead of 6 px. Report [dc_mow5mjh10x](2026-11-06-toasts-now-paint-above-open-sheets-on-live-24984fc-w5mjh10x.md).

**What you'd see:** In the Town Hall in-tray with a sheet open, any error toast appears at the bottom left over the sheet's text (crops mf_iq1ukysx9m laptop, mf_qya0wtso0y phone).

**Your call:** None.

## Decided
- [dc_k0lx8h2hwa](2026-11-06-pr-391-disclosure-census-panel-folds-merged-as-249-lx8h2hwa.md) → approve (PR #391 merged as 24984fc6; live census parked on its deploy)
- [dc_mow5mjh10x](2026-11-06-toasts-now-paint-above-open-sheets-on-live-24984fc-w5mjh10x.md) → approve (toasts above sheets pass on live at both sizes; flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md) fixed)
- [dc_0gcm0c3lhh](2026-11-06-kr-p6l1w6tade-on-live-24984fc6-all-70-counted-rows-cm0c3lhh.md) → approve (live census 70/70, mock 82/82; kr_p6l1w6tade claimed; grant closed as done)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_zak30564zh (progressive disclosure, closed done) | kr_obykl8yydh grant page opens on a summary | met | 1,269,664 / 2,000,000 (730,336 returned) |
| | kr_3jie8qwdt6 goal tree opens on the goal | met | |
| | kr_p6l1w6tade disclosure census passes every non-document panel | met | |
| gr_4csjpgh346 (sidebars and sheets, funded) | kr_xnt1h13yce one shared Sheet | on-track, evidence in hand | see the grant card / 1,500,000 |
| | kr_gg1wjnt07k in-tray and cabinet items in a sheet | on-track, evidence in hand | |
| | kr_sa1gn36ndz links open the link sheet | on-track, evidence in hand | |
| | kr_pm0fmsiaxs rich HTML + sandboxed page docs | on-track, evidence in hand | |
| | kr_nokx342ovj the rule in the style guide and docs/ | not-started (check scheduled 2026-11-14 10:00 UTC, sc_91et8n5w5r) | |

Spend today by lane (at the start of this session): exploration 38,216 tokens; directed 126,609 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_irjtu6tknu), 0 requests, 1 rollup ([dc_0ju8ttlazs](2026-11-06-one-design-is-done-every-screen-now-uses-one-type-u8ttlazs.md))._
