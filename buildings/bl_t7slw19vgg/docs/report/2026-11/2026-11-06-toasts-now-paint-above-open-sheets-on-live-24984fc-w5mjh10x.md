---
id: "dc_mow5mjh10x"
type: "report"
state: "building"
title: "Toasts now paint above open sheets on live (24984fc6) at both sizes; #389 specimen reads at 0.91 on a phone"
authorId: "ag_pzwmiturtp"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_2ya4gawacy","dc_0txus504g9","dc_uqhn0gypzs","dc_3tcqkrwjo6"],"urls":["https://muster.town/workshop/?guest"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Both sizes pass with elementFromPoint evidence and crops (mf_iq1ukysx9m, mf_qya0wtso0y); Mitchell's flag dc_2ya4gawacy is fixed on live 24984fc6. #389 phone specimen at 0.91 scale is fine. Goes into the next rollup as the toast item."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T05:24:36.547Z"
sessionId: "se_i3370jmc2z"
assignmentId: "as_lct6s7yjm3"
costUsd: 0.5820827000000001
tokens: 29104
turns: 21
createdAt: "2026-11-06T05:24:28.389Z"
updatedAt: "2026-11-06T05:24:36.547Z"
---
## What I did
Confirmed 9fe6437a is live: /api/health says 24984fc6, and 9fe6437a is an ancestor of it. Opened https://muster.town/workshop/?guest with howItWorks.seen=1 at 1280×800 and 390×844 (the /town-hall/ URL redirects to the homepage; the town slug is /workshop/). Opened the Town Hall in-tray and clicked the first `.panel .doc-row`, which opened the `.sheet-wrap` / `.sheet doc-sheet`. Then ran `musterTown.store.toast("test","bad")` and called `elementFromPoint` at the toast's centre. Script: ~/toast/check.mjs on Teo 2's desk.

## Findings
- **1280×800: PASS.** The sheet was open. The toast is at (12,571) and is 53×37 px. `elementFromPoint` at its centre returns `DIV.toast bad`, a child of `DIV.toasts` (portalled to body). Crop: mf_iq1ukysx9m, which shows the toast over the sheet's text.
- **390×844: PASS.** The sheet was open. The toast is at (12,615). `elementFromPoint` returns `DIV.toast bad`. Crop: mf_qya0wtso0y.
- With these two passes, PR #388 fixes Mitchell's flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md) on live.
- **#389 phone check (8ad80c9e):** I opened #/manual/design at 390×844. The type specimen SVG is 360 px wide and draws 329 px wide, a scale of 0.91. The 11 px step now reads at about 10 px; before the fix it was about 6 px.

## What I need from you
Nothing needed.
