---
id: "dc_v4itjbkgfi"
type: "wiki"
state: "building"
title: "Bank interior: tabs and room objects"
authorId: "ag_zk2z9wqy4d"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-10-30T19:04:41.399Z"
updatedAt: "2026-10-30T19:04:41.399Z"
---
Mitchell asked for this in 1:1 mt_ew2d0mm7h9 (notes [dc_5qmjtowif6](../../../../bl_xvgnd1fvh6/docs/meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-cleo-notes-mjtowif6.md)): break the Bank page into tabs, give each tab a physical object in the room, and drop the big counter.

**Now true:** merged on origin/main as f402bcf (PR #119). Redeploy queued 2026-10-30; not yet verified live.
- The tabs are `BANK_TABS` in `packages/schema/src/index.ts`. Each tab and its object:
  - Overview: the vault, place `bank`
  - Tokens & sources: the ledger desk, `bank:ledger`
  - Pools: the fountain, `bank:pools`
  - Spending: the spending board, `bank:spending`; the tab also holds drift and the out-of-tokens deaths and cap
  - Hosting: the server rack, `bank:hosting`
- The places come from `BANK_FIXTURES.stations` through `bankPlaces()`. Core layout and the web mock share it. `bankTabOf(placeId)` gives a place's tab.
- In `renderer.ts`, `PLACE_PANEL.bank` passes `tab`. `app.tsx` keys BankPanel per open (openSeq), so a deep-link lands on its tab.
- Tiles BANK_LEDGER, BANK_FOUNTAIN, BANK_SPENDING and BANK_SERVER are 22–25. Their sprites are in `map/sprites.ts`. The teller counter and `drawGoldCounter` are gone.
- `BankView({tab,…})` in `BankPanel.tsx` renders one tab followed by the FinanceFooter. `web/test/finance.test.tsx` asserts which sections each tab holds.
- docs/manual.md is at 1,899 of its 1,900-word cap.

**Not done:** the generic building-panel interior.
