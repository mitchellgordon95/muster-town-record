---
id: "dc_j8yjsnvamu"
type: "report"
state: "building"
title: "Fountain polish: Bank sign fits its lawn at any zoom, phone toolbar moved to the bottom (PR #220), parked on CI"
authorId: "ag_8m3upwyzwt"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Good diagnosis. The merge, redeploy and live check is already parked as as_55s7k3cncd (waits on PR #220 CI)."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-31T22:33:44.736Z"
sessionId: "se_uu0500c6un"
assignmentId: "as_1yxoufc9ex"
costUsd: 1.7826337999999997
tokens: 89132
turns: 52
createdAt: "2026-10-31T22:33:39.435Z"
updatedAt: "2026-10-31T22:33:44.736Z"
---
## What I did
- Reproduced both defects on live and found what causes each. Fixed both in one PR: https://github.com/mitchellgordon95/muster-town/pull/220 (draft, CI running).
- Checked the fix with the dev web client running against live data (the live map is on the fountain shape): typecheck passes and the web tests pass (206/206). Rewrote topic page [dc_004hyy29z6](../../wiki/2026-10/2026-10-31-town-layout-doors-on-any-side-the-planned-fountain-4hyy29z6.md).

## Findings
- **Bank sign, cause:** the marquee is drawn at a fixed screen size, about 350 px wide. At the default zoom 3 it fits the 8 free lawn tiles between the Bank and UI/UX, with one tile to spare. At zoom 2 (the "−" key) it needs about 11 tiles, so it covered UI/UX. That is the earlier "laptop" screenshot.
- **Bank sign, fix:** `drawBankSign` takes a `maxW`. The renderer passes the clear width up to the next building lot on the rows the sign covers, minus one tile, and the sign scales down to fit (never below half size). Because this works from the lots themselves, it holds in every shape and at any zoom. Dev check at 1280×720: zoom 3 looks the same as before; at zoom 2 the sign now ends a tile short of UI/UX.
- **Phone toolbar:** at ≤760 px the town-map toolbar (and the room editor's, which uses the same class) now sits at the bottom of the screen with its title stacked. The "Tap: …" hint is hidden while town planning is open. Dev check at 390×844: the HUD is at the top, the toolbar at the bottom, and they don't overlap.
- **Noticed, not fixed:** on phone, town planning doesn't fit the whole town in the width (the west districts are cut off). The phone "lands inside a building" issue is left to gr_ukrou4zjha, as asked.

## What I need from you
Nothing needed. I'll resume when CI finishes, then merge, redeploy and check live.
