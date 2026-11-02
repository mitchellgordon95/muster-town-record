---
id: "dc_7xm0lcxcrf"
type: "report"
state: "building"
title: "Bank marquee moved off the Town Hall's wall (PR #124, 5ea10f0); live check parked"
authorId: "ag_b2h51itymm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Marquee moved left of the Bank (web only, no layout change, tree test added), PR #124 merged as 5ea10f0, redeploy queued. The live check and crop are already parked as as_0lnilemil4 on deploy 5ea10f0; its report goes into rollup 33's Shipped item 2 as the fix for the known flaw."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T22:25:21.890Z"
sessionId: "se_t1zjczo0oi"
assignmentId: "as_7ygswfxwpa"
costUsd: 0.8679447999999998
tokens: 43397
turns: 27
createdAt: "2026-10-30T22:25:13.010Z"
updatedAt: "2026-10-30T22:25:21.890Z"
---
## What I did
- Found the cause and moved the Bank's marquee.
- Added a tree layout test.
- Opened PR #124 (https://github.com/mitchellgordon95/muster-town/pull/124). CI passed, so I merged it as **5ea10f0** and queued a redeploy.
- The live check and the picture are parked until 5ea10f0 is live.

## Findings
- **Cause:** the marquee is drawn in screen pixels. It is 112 px tall and sits 5 world px (15 screen px) above the Bank's door, so it needs about 127 px.
  - The tree layout leaves only the root plaza's 2 rows between the Town Hall and the Bank (`core/world/tree.ts`, BANK_LOT y 14, hall bottom row 11).
  - Those 2 rows are 96 px at zoom 3 and 64 px at zoom 2, so no gap constant would fit the marquee at every zoom.
  - Moving BANK_LOT down would shift every child band, which the assignment ruled out.
- **Fix (web only):** the marquee now hangs left of the Bank.
  - Its right edge sits one grass column left of the root's trunk road (x = BANK_LOT.x − 4) and it is centred on the Bank's rows.
  - The layout always leaves that grass empty: the root's own labs hang right of the Bank, and children start below it.
  - Code: `drawBankSign` gained a `right` anchor (`web/src/map/overlay.ts`), and the call site changed (`web/src/map/renderer.ts`).
  - No layout constant changed, nothing else moved, no migration, no Bank accounting change. `tree.ts` is untouched, which keeps clear of step 3's files.
- **Test:** `core/test/tree.test.ts` has a new case. It checks that a 20-column band left of the Bank, across the Bank's rows, holds no lot, plaza or road on the live tree.
  - typecheck passes, tree tests pass 7/7, CI check passes.
- **Not yet verified:** I have not looked at the marquee in a browser.
- **Plan for the continuation:**
  1. Confirm `git merge-base --is-ancestor 5ea10f0 <health commit>` passes.
  2. Screenshot https://muster.town/workshop/ around the Town Hall and the Bank using the screenshot-live-town skill.
  3. Confirm the marquee is clear of the hall's wall and of the trunk road.
  4. Upload one crop of ≤300 px tall for rollup 33.

## What I need from you
Nothing needed.
