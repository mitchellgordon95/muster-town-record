---
id: "dc_xggewkamm8"
type: "report"
state: "building"
title: "Content now opens in one centred sheet (Bank, in-tray items, every doc/grant/agent link), docs keep rich HTML, and the bulletin board shows a red badge for unread notes (your flag): all live on 2a279a1d"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_qefnwr058y","dc_ep5efd8r14","dc_mvftzmjuyt","dc_cv0n2rw5mp","dc_rg9rkfnwfp","dc_mcpu0rdlpr","dc_xautttt3vc","dc_d662kzv42m","dc_82s3ebqysm","dc_2iazdl2w4h","dc_3s2x7xfpzf","dc_oo2x7yaevb","dc_8bv39n63k1","dc_xnswxyaorl","dc_5f80lz5gdx","dc_j6c6a2z5gp","dc_dw0tdr0a6k","dc_0mdearrlgy","dc_ovw3kn4elt","dc_yyn0y99ph4","dc_4ob45egack","dc_b33q0pr9ht"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/371","https://github.com/mitchellgordon95/muster-town/pull/374","https://github.com/mitchellgordon95/muster-town/pull/375","https://github.com/mitchellgordon95/muster-town/pull/376","https://github.com/mitchellgordon95/muster-town/pull/378","https://github.com/mitchellgordon95/muster-town/pull/379","https://github.com/mitchellgordon95/muster-town/pull/368"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-06T04:34:01.874Z"
sessionId: "se_f2rk5zsvbb"
createdAt: "2026-11-06T00:14:22.346Z"
updatedAt: "2026-11-06T04:34:01.874Z"
---
Live: 2a279a1d (since 2026-11-06 00:11 UTC). Everything below was checked on live as a guest at 1280×800 and 390×844.

## Shipped

**1. Content opens in one centred sheet; lists and chats stay at the side**

**What it is:** Your rule from the 1:1 ("sidebars for navigation and detail, central modals for content") is now how the town works. The Bank, the goal editor, any in-tray or filing-cabinet item, and every link to a doc, grant or agent open in one shared centred sheet; the list you came from stays open beside it, and Esc closes only the newest sheet. Doc bylines name retired forks ("by Teo 1", not "by ag_…"). Grant gr_4csjpgh346 steps 1–3 and the byline fix: PRs #371, #374, #376, #379; reports [dc_xautttt3vc](2026-11-05-the-bank-opens-in-the-shared-sheet-on-live-21cdbd5-utttt3vc.md), [dc_xnswxyaorl](2026-11-05-in-tray-and-filing-cabinet-items-open-in-the-sheet-swxyaorl.md), [dc_dw0tdr0a6k](2026-11-05-links-open-in-a-centred-sheet-on-live-pr-376-de097-0tdr0a6k.md), [dc_b33q0pr9ht](2026-11-06-doc-bylines-show-the-fork-s-name-on-live-2a279a1d-3q0pr9ht.md).

**What you'd see:** Open the Town Hall in-tray and click a row: on a laptop the item is a 779×760 sheet with the 461 px list still showing on the right and the row highlighted; on a phone it fills the screen. Click a gr_ link inside it: the grant opens on top, one Esc closes it, a second closes the item, the list never goes away. `#/bank` is a 1240×760 sheet with its five tabs; 0 old bank/goal-editor shells remain in the page. The delight walk reaches 12 of 12 first-visit moments through the new sheets (PR #378).

![A grant link opened from an in-tray item as a centred sheet on laptop, the in-tray list still visible beside it](/api/media/mf_bw347aegy1.png)

**Your call:** None.

**2. Docs keep their rich HTML, and a "page" doc runs its own script in a sandbox**

**What it is:** Step 4 of the same grant (PR #375, fcdb0254): the sanitizer no longer strips a doc's layout, and the new doc type "page" opens inside the sheet in an iframe with scripts allowed but no network and no access to the town, as you agreed ("sgtm"). Reports [dc_2iazdl2w4h](2026-11-05-docs-keep-rich-html-doc-type-page-opens-in-a-sandb-azdl2w4h.md), [dc_oo2x7yaevb](2026-11-05-pr-375-rich-html-doc-type-page-merged-as-fcdb0254-2x7yaevb.md), [dc_8bv39n63k1](2026-11-05-sample-page-dc-h8n2kves0x-is-live-and-runs-its-scr-v39n63k1.md).

**What you'd see:** The library has a sample page, "Bank balance over time" ([dc_h8n2kves0x](../../../../../library/page/2026-11/2026-11-05-bank-balance-over-a-week-sample-page-n2kves0x.md)): open it and its chart draws itself from an inline script, inside the sheet, at both sizes. No picture here (the one-picture-per-item limit is spent on items 1 and 3; crop mf_jc8wfp4s4g is on the report).

**Your call:** None.

**3. The bulletin board tracks what you've read and shows a red badge for unread notes (your flag)**

**What it is:** Your flag [dc_04q4h8s229](../../flag/2026-11/2026-11-05-nit-can-i-get-a-read-unread-tracker-for-the-bullet-q4h8s229.md) ("a read/unread tracker for the bulletin board by user, and a red badge for unreads"). Each signed-in human has their own read marks; a note you posted counts as read for you; a note taken down and pinned again stays read. PR #368 (06d732a3), reports [dc_qefnwr058y](2026-11-05-bulletin-board-read-unread-per-human-red-badge-pr-fnwr058y.md), [dc_mvftzmjuyt](2026-11-05-pr-368-had-merge-conflicts-with-main-resolved-migr-ftzmjuyt.md), [dc_rg9rkfnwfp](2026-11-05-pr-368-bulletin-read-unread-red-badge-merged-as-06-9rkfnwfp.md), [dc_d662kzv42m](2026-11-05-bulletin-read-unread-red-badge-pr-368-live-at-bcea-62kzv42m.md).

**What you'd see:** On the map, the bulletin board carries a red count of your unread notes and each unread row has a red "new" pill; opening the note clears it. Live has no notes pinned yet, so the badge was verified signed-in on the mock and the routes on live (guests get no read marks and `POST /api/bulletin/all/read` refuses them). Pin one note and any other signed-in human sees the badge.

![The bulletin board with a red "1" badge, the unread row's "new" pill, and the board with no badge after the note is opened](/api/media/mf_bqqey2sm8a.png)

**Your call:** None.

## Decided
- [dc_qefnwr058y](2026-11-05-bulletin-board-read-unread-per-human-red-badge-pr-fnwr058y.md) → approve (PR #368 opened, parked on CI)
- [dc_ep5efd8r14](2026-11-05-sheet-grant-gr-4csjpgh346-1-5m-cut-into-5-steps-st-5efd8r14.md) → approve (Sheet grant cut into 5 steps, step 1 queued)
- dc_mvftzmjyt → see [dc_mvftzmjuyt](2026-11-05-pr-368-had-merge-conflicts-with-main-resolved-migr-ftzmjuyt.md) → approve (PR #368 conflicts resolved, migration renumbered 095)
- [dc_cv0n2rw5mp](2026-11-05-one-shared-sheet-the-bank-and-the-goal-editor-open-0n2rw5mp.md) → approve (PR #371 draft, parked on CI)
- [dc_rg9rkfnwfp](2026-11-05-pr-368-bulletin-read-unread-red-badge-merged-as-06-9rkfnwfp.md) → approve (PR #368 merged as 06d732a3)
- [dc_mcpu0rdlpr](2026-11-05-pr-371-one-shared-sheet-for-the-bank-and-goal-edit-pu0rdlpr.md) → approve (PR #371 merged as 21cdbd51)
- [dc_xautttt3vc](2026-11-05-the-bank-opens-in-the-shared-sheet-on-live-21cdbd5-utttt3vc.md) → approve (Bank sheet live, step 1 done)
- [dc_d662kzv42m](2026-11-05-bulletin-read-unread-red-badge-pr-368-live-at-bcea-62kzv42m.md) → approve (bulletin badge live, flag done)
- [dc_82s3ebqysm](2026-11-05-in-tray-and-filing-cabinet-items-open-as-a-centred-s3ebqysm.md) → approve (PR #374 draft, parked on CI)
- [dc_2iazdl2w4h](2026-11-05-docs-keep-rich-html-doc-type-page-opens-in-a-sandb-azdl2w4h.md) → approve (PR #375 draft, parked on CI)
- [dc_3s2x7xfpzf](2026-11-05-pr-374-in-tray-and-filing-cabinet-items-open-in-th-2x7xfpzf.md) → approve (PR #374 merged as 5b02820a)
- [dc_oo2x7yaevb](2026-11-05-pr-375-rich-html-doc-type-page-merged-as-fcdb0254-2x7yaevb.md) → approve (PR #375 merged as fcdb0254)
- [dc_8bv39n63k1](2026-11-05-sample-page-dc-h8n2kves0x-is-live-and-runs-its-scr-v39n63k1.md) → approve (sample page live; promoted to the library)
- [dc_xnswxyaorl](2026-11-05-in-tray-and-filing-cabinet-items-open-in-the-sheet-swxyaorl.md) → approve (in-tray/cabinet sheet live, step 2 done)
- [dc_5f80lz5gdx](2026-11-05-links-to-docs-grants-and-agents-open-in-a-centred-80lz5gdx.md) → approve (PR #376 draft, parked on CI)
- [dc_j6c6a2z5gp](2026-11-05-pr-376-links-open-in-a-centred-sheet-merged-as-de0-c6a2z5gp.md) → approve (PR #376 merged as de097e16)
- [dc_dw0tdr0a6k](2026-11-05-links-open-in-a-centred-sheet-on-live-pr-376-de097-0tdr0a6k.md) → approve (link sheet live, step 3 done; delight-walk fix queued)
- [dc_0mdearrlgy](2026-11-05-delight-walk-mjs-looks-for-the-centred-sheet-12-12-dearrlgy.md) → approve (PR #378 delight-walk, parked on CI)
- [dc_ovw3kn4elt](2026-11-05-doc-bylines-show-a-retired-fork-s-name-instead-of-w3kn4elt.md) → approve (PR #379 bylines opened)
- [dc_yyn0y99ph4](2026-11-05-pr-378-delight-walk-mjs-handles-centred-sheets-mer-n0y99ph4.md) → approve (PR #378 merged as dd7accb4, script only)
- [dc_4ob45egack](2026-11-06-pr-379-doc-bylines-show-a-retired-fork-s-name-merg-b45egack.md) → approve (PR #379 merged as 2a279a1d)
- [dc_b33q0pr9ht](2026-11-06-doc-bylines-show-the-fork-s-name-on-live-2a279a1d-3q0pr9ht.md) → approve (bylines live at both sizes)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_4csjpgh346 (sidebars and sheets, funded) | kr_xnt1h13yce one shared Sheet: Bank + goal editor | on-track, evidence in hand (claimed at checkpoint or close) | see the grant card / 1,500,000 (about 15 sessions booked so far, roughly 0.5 M by their reports) |
| | kr_gg1wjnt07k in-tray and cabinet items open in a sheet | on-track, evidence in hand | |
| | kr_sa1gn36ndz links open the link sheet | on-track, evidence in hand | |
| | kr_pm0fmsiaxs rich HTML + sandboxed page docs | on-track, evidence in hand | |
| | kr_nokx342ovj the rule in the style guide and docs/ | not-started (wording with Kelly; check scheduled 2026-11-14) | |
| gr_kvmwutmybu (one design, at checkpoint) | kr_w9t4cey0l2 no dim text | claimed | 821,388 / 600,000 |
| | kr_68eg5yskoo one type scale | claimed | |
| | kr_qge1yo1lmi one palette | claimed | |
| | kr_mmdday2x7z signed-in views match | on-track (PR #350 merge held at the checkpoint) | |
| | kr_z4junko6nt manual Design section | not-started (in PR #350) | |
| gr_zak30564zh (progressive disclosure, at checkpoint) | kr_obykl8yydh grant page summary | claimed | 1,034,255 / 800,000 |
| | kr_3jie8qwdt6 goal tree opens on the goal | claimed | |
| | kr_p6l1w6tade disclosure census passes | at-risk | |

Spend today by lane (before this session): exploration 14,083 tokens; directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_irjtu6tknu), 0 requests, 1 rollup ([dc_8jre4dz65a](2026-11-05-chat-history-is-back-in-full-meeting-transcripts-a-re4dz65a.md))._
