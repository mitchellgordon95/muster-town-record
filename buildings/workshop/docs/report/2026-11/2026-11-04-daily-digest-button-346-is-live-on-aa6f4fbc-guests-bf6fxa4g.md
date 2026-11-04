---
id: "dc_95bf6fxa4g"
type: "report"
state: "building"
title: "Daily digest button (#346) is live on aa6f4fbc: guests get no digestRun and no button"
authorId: "ag_9cxqzrqskd"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "#346 live on aa6f4fbc confirmed (guest: no digestRun, no button; POST /api/digest/run → 401). Goes into rollup 47 as live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T22:19:02.974Z"
sessionId: "se_qvqr6and7y"
assignmentId: "as_ejx98ofqlj"
costUsd: 0.28254310000000005
tokens: 14127
turns: 6
createdAt: "2026-11-04T22:18:54.641Z"
updatedAt: "2026-11-04T22:19:02.974Z"
---
## What I did
Checked the live town from outside, signed out. I read /api/health, the guest in-tray API, the unauthenticated run endpoint, the live JS bundle, and the button code.

## Findings
- **Live:** /api/health at 22:18:42Z reports commit aa6f4fbc (startedAt 20:40:25Z), and dd99c595 is an ancestor of it. PR #346 is therefore live.
- **Guest:** `GET /api/buildings/town-hall/intray` returns `digestRun: null`. `DailyDigestButton` (packages/web/src/panels/Places.tsx:125) returns null when `run` is null, so a guest sees no "Daily digest" button. `POST /api/digest/run` with no token returns 401 "Missing or invalid bearer token".
- The live bundle (main-CXHicM_s.js) contains the "Daily digest" label. The button sits next to Talk to Secretary in the in-tray header.
- **Not checked live:** the signed-in admin side (button visible, enabled once the retainer is approved and a rollup is new). A headless browser here cannot sign in. That side is covered by the server and web tests that were merged with #346. The button should go into rollup 47 as live, and Mitchell sees it as soon as he opens the Town Hall in-tray.

## What I need from you
Nothing needed.
