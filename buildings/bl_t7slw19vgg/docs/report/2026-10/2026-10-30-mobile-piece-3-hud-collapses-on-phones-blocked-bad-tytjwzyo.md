---
id: "dc_yztytjwzyo"
type: "report"
state: "building"
title: "Mobile piece 3: HUD collapses on phones; blocked-badge reasons open on tap (merged fa48254, PR #106)"
authorId: "ag_8qk70wzbpa"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["mt_jzoyqe2lea","dc_wkn26bpdx0","dc_he1xwen6a5"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/106"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Mobile piece 3 is done: the HUD collapses on phones and blocked reasons open on tap (fa48254). This finishes the mobile set Mitchell asked for (mt_jzoyqe2lea). The hover tip for forks is out of scope because the panel already covers it."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-30T00:09:16.390Z"
sessionId: "se_42u88ctubk"
assignmentId: "as_zgg7llih77"
costUsd: 1.0032780000000003
tokens: 50164
turns: 34
createdAt: "2026-10-30T00:08:53.461Z"
updatedAt: "2026-10-30T00:09:16.390Z"
---
## What I did
Before starting, I confirmed that piece 2 (23f2ead) was live. I made the two fixes in `packages/web` (hud.tsx, MapCanvas.tsx, renderer.ts, styles.css) and opened PR https://github.com/mitchellgordon95/muster-town/pull/106. CI passed and I merged it as **fa48254**. I queued a redeploy, so **fa48254 should be live**; I haven't checked that yet. I updated the topic page [dc_he1xwen6a5](../../wiki/2026-10/2026-10-29-mobile-touch-on-the-town-map-1xwen6a5.md).

## Findings
- **HUD card:** at 760 px wide or less, a signed-in member's card now starts collapsed. It is one line, about 55 px tall, where the expanded card was about 400 px at 390×844. The ▾ toggle still expands it, and the notice-count dot shows while it is collapsed. Guests still get their short card (at most 35% of the screen) because it holds Sign in.
- **Blocked reasons on touch:** the first tap on a red "blocked N" badge (or a "scheduled N" badge) shows its reasons card, which now ends "(tap again for the queue)". A second tap opens the queue, and tapping anywhere else clears the card. Mouse clicks still open the queue straight away; I checked this at 1280×800.
- **How I checked it:** mock mode, playwright at 390×844 with touch:
  - HUD class is `hud collapsed`, 55 px tall.
  - Tapping Noor's "blocked 2" badge showed her reasons card with no panel open.
  - A second tap opened Noor's panel.
  - A tap on the ground cleared the card.
  - Expanding the HUD gave 400 px.
  - Typecheck and the web tests (141) pass.
- Screenshot (phone, collapsed HUD, the reasons card after a tap): ![Phone 390px: HUD collapsed, tapped blocked badge shows its reasons](/api/media/mf_miazo607ke.png)
- **Gap left:** the fork tip that shows when you hover a fork agent doesn't appear on touch. Tapping the agent opens its panel, which shows the same information, so I left it.

## What I need from you
Nothing needed.
