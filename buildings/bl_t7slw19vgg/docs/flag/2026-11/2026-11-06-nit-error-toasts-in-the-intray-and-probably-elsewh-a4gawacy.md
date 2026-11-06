---
id: "dc_2ya4gawacy"
type: "flag"
state: "building"
title: "nit: error toasts in the intray (and probably elsewhere) have a lower z index than the main content modal so you can't …"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_2ya4gawacy): \"error toasts in the intray (and probably elsewhere) have a lower z index than the main content modal so you can't see them without dismissing\". Cause, from main at 5dc50c7: `.toasts` (packages/web/src/styles.css:128) is position:absolute with no z-index, and `<Toasts />` renders at packages/web/src/app.tsx:335, before the sheets (HowItWorks, ManualSheet, GoalTreePanel, BankSheet, LinkSheet at app.tsx:336-342). The centred sheet `.sheet-wrap` is fixed with z-index 30 (styles.css:957) and its backdrop covers the bottom-left where toasts sit; the help/manual overlays use z-index 40-41 (packages/web/src/panels/hiw.css:5,74,93). So any toast fired while a sheet is open (an in-tray action that fails, a key-result mark, a counter) is hidden under the sheet. Fix: give `.toasts` a z-index above every overlay (e.g. 50, and note it in the comment at styles.css:114 alongside the minimap/hud note) and move `<Toasts />` to the last child of `.app` in app.tsx so DOM order agrees; check nothing else (`.layout-bar` z 20, `.help-tip` z 41) needs to sit above a toast. Keep toasts pointer-events as they are so the sheet stays usable behind them. Open a PR, merge it when green (no redeploy), park on {deploy: sha}, then verify live as a guest: open the Town Hall in-tray sheet, trigger an error toast (e.g. an action that fails for a guest, or `store.toast` via the console is fine if nothing natural fires) and crop a picture showing the toast on top of the open sheet at laptop and phone size. Report with the PR number, the sha and the crop."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T04:17:25.263Z"
flagPos: {"x":82,"y":12}
pickedUpAt: "2026-11-06T04:16:58.794Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-06T04:16:44.258Z"
updatedAt: "2026-11-06T04:17:25.263Z"
---
nit: error toasts in the intray (and probably elsewhere) have a lower z index than the main content modal so you can't see them without dismissing
