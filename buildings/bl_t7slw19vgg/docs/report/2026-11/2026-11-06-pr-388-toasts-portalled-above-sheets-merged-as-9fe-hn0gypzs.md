---
id: "dc_uqhn0gypzs"
type: "report"
state: "building"
title: "PR #388 (toasts portalled above sheets) merged as 9fe6437a; live check still to do"
authorId: "ag_z7iveowcpv"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "#388 merged as 9fe6437a; the live check goes on the queue as its own assignment parked on {deploy: 9fe6437a}."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T05:00:28.464Z"
sessionId: "se_nrlcmvhoe7"
assignmentId: "as_hfppcyh89u"
costUsd: 0.28904420000000003
tokens: 14452
turns: 5
createdAt: "2026-11-06T05:00:10.594Z"
updatedAt: "2026-11-06T05:00:28.464Z"
---
## What I did
PR #388's CI passed (check and image green). I marked it ready and merged it as **9fe6437a**. I did not call redeploy. The live server runs 41c5e7d, which doesn't include the merge yet. This chain has already parked three times in a row, so I can't park it again: someone needs to queue the live check below once 9fe6437a is live.

## Findings
- #388 renders the toasts through a portal to `<body>` with `position: fixed; z-index: 50`. The sheets use z-index 30, so a toast now paints on top of an open sheet. The earlier fix (#385) didn't work because `.app` is `position: fixed`, which trapped the toast below the sheets.
- Live check still to do. Teo can assign it with waitFor `{deploy: "9fe6437ae7eece0259198a4df4c599644ea0a5e1"}`:
  1. Open https://muster.town/town-hall/?guest as a guest, first setting localStorage `musterTown.howItWorks.seen=1`.
  2. Open the in-tray and click the first `.panel .doc-row` so the sheet opens.
  3. Fire `musterTown.store.toast("test", "bad")`.
  4. At 1280×800 and 390×844, check that `elementFromPoint` at the toast's centre returns the toast, and crop both sizes for Mitchell's flag [dc_2ya4gawacy](../../flag/2026-11/2026-11-06-nit-error-toasts-in-the-intray-and-probably-elsewh-a4gawacy.md).
  - Tools: playwright-core in /tmp/pw and /usr/bin/chromium.

## What I need from you
Nothing needed.
