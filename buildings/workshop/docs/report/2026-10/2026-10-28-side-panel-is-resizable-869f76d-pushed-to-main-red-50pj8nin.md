---
id: "dc_7d50pj8nin"
type: "report"
state: "building"
title: "Side panel is resizable (869f76d pushed to main, redeploy queued)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "869f76d is live (health commit at ~19:50Z). Root is parked for its own live check, so no second assignment; goes under Shipped in rollup 29 with Mitchell's flag dc_ew132qg6jk. Root's self-harvest assignment follows once that check lands."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T19:22:28.831Z"
sessionId: "se_ks9iejwzhu"
assignmentId: "as_zpkxixuzbg"
costUsd: 0.5483503
tokens: 27418
turns: 15
createdAt: "2026-10-28T18:50:41.309Z"
updatedAt: "2026-10-28T19:22:28.831Z"
---
## What I did
Built Mitchell's flag [dc_ew132qg6jk](../../flag/2026-10/2026-10-28-i-d-like-to-be-able-to-resize-the-side-panel-when-132qg6jk.md) ("resize the side panel when reading docs"). Committed 869f76d straight to main, pushed it and queued the redeploy. **869f76d should be live** once the server restarts. I'm parked until that deploy, then I'll do the live check.

## Findings
- **Drag handle:** the left edge of the side panel can now be dragged. It's an 8px strip that highlights on hover or while dragging, and the cursor changes to the resize arrow. The code is in `packages/web/src/panels/panelResize.tsx`, and `app.tsx` now takes the panel width from `usePanelWidth()`.
- **Limits:** the panel can't go narrower than 320px. It can't go wider than 1400px or the window width minus 240px, whichever is smaller, so some map always shows. If the window shrinks, the saved width is squeezed to fit but not forgotten.
- **Remembered width:** the chosen width is saved in the browser's localStorage under `musterTown.panel.width`, so it survives reloads.
- **Reset:** double-click the handle (or press Home on it) to clear the saved width. The panel goes back to the old default of about 36% of the window, between 360 and 500px.
- **Keyboard:** the left and right arrow keys widen or narrow the panel by 40px.
- **Phones:** on screens 760px wide or less the panel stays full width and the handle is hidden.
- **No clipping:** making the panel wider only reflows the text. Nothing inside the panel has a fixed width, so nothing gets cut off (the standing rule [dc_w6e1vpbkuf](../../wiki/2026-10/2026-10-28-workshop-standing-rules-e1vpbkuf.md)).
- **Checks:** the new test `packages/web/test/panelResize.test.tsx` covers how the handle is drawn, the limits, saving and reloading, and the reset. All web tests pass (101), the typecheck is clean and the Vite build works. I haven't seen the panel in a real browser, because there's no browser on my desk.

## What I need from you
Nothing needed.
