---
id: "dc_ykm8ki18qv"
type: "report"
state: "building"
title: "Toasts over open sheets: PR #385 open, parked on CI"
authorId: "ag_cgg092p8ua"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #385 open (toasts z-index 50, Toasts last in .app); its continuation as_0ffnvmv3do waits on {pr: 385} and then merges, parks on deploy and verifies live with crops. Nothing more to add."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T04:20:49.005Z"
sessionId: "se_76nsjry3b0"
assignmentId: "as_0rsygihgty"
costUsd: 0.3728754
tokens: 18644
turns: 7
createdAt: "2026-11-06T04:19:24.411Z"
updatedAt: "2026-11-06T04:20:49.005Z"
---
## What I did
Fixed Mitchell's flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md) (error toasts hidden under the in-tray sheet) and opened draft PR #385: https://github.com/mitchellgordon95/muster-town/pull/385

## Findings
- Cause as briefed: `.toasts` (styles.css) had no z-index and `<Toasts />` rendered before the sheets; `.sheet-wrap` is z 30, help/manual 40–41, `.layout-bar` 20. `.panel` has no z-index, so a side panel's own sheet stacks in `.app` too.
- Change: `.toasts` gets `z-index: 50`; stacking order is written in the comment above `.minimap`; `<Toasts />` moved to the last overlay in app.tsx (before the mock badge). Pointer-events unchanged (container none, toast auto), so the sheet behind stays usable.
- Checks: typecheck passes, web tests 379/379, check:css 0 stray values.
- Next session: if CI is green, mark ready, merge (no redeploy), park on {deploy: merge sha}; then as a guest on live open the Town Hall in-tray sheet, fire a toast (`store.toast` via console if nothing natural fails) and crop at 1280×800 and 390×844.

## What I need from you
Nothing needed.
