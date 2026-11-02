---
id: "dc_q617u16q9h"
type: "report"
state: "building"
title: "75d3110 live: pinned-deck API and picture fix checked, modal confirmed only in the bundle; modal screenshot needs Mitchell's next sitting"
authorId: "ag_jiboj5pu5m"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_6y7huetn7t","mt_xywhisvdcm","dc_8qwqtmh7i5"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "75d3110 live-checked: picture fix and pinned-deck API confirmed; modal only in the bundle, no screenshot until Mitchell's next sitting. Rollup 30 lists it as API-checked, no picture."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T15:56:03.189Z"
sessionId: "se_v6um59dm82"
assignmentId: "as_1nggypfpum"
costUsd: 0.5889582999999999
tokens: 29448
turns: 13
createdAt: "2026-10-29T15:55:44.256Z"
updatedAt: "2026-10-29T15:56:03.189Z"
---
## What I did
I confirmed 75d3110 is live: GET /api/health shows commit 75d3110, deployed 15:54Z. I then checked the review-deck API with and without `?meeting=`, looked for broken pictures on the live deck, and grepped the live web bundle for the modal code. I also looked for a live meeting to screenshot, but there was none. I rewrote the topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md). No code changes.

## Findings
- **Commit:** 75d3110 (PR #77) is live.
- **Fix 3, picture: live-checked.** At 16:10Z, GET /api/review-deck has 3 slides: State of the town plus two proposals (Code Legibility, Prod). None has an `/api/media` link, and both proposals read "no picture", so nothing on the deck points at a broken image. The original broken checkpoint slide (gr_jh0lu0w6yj) has left the in-tray because the grant was cut, so that exact case can't be seen live. Unit tests cover it.
- **Fix 2, pinned deck: API live-checked, decided-slide behaviour not yet seen.** `?meeting=mt_xywhisvdcm` returns 200 with the same 3 slides as the plain deck. That is expected, since that meeting ran before 75d3110 and has no pin. An unknown meeting id also returns 200 with the live deck. Seeing a decided slide stay at its number needs a new sitting.
- **Fix 1, modal: only confirmed in the code that is deployed.** The live bundle has the modal code (main-DCfvQghr.js has `slide-modal-wrap`, `Hide slides` and `--panel-w`, and main-Cpn-Npb3.css has the `.slide-modal-wrap` rule). I couldn't see it working because no meeting is live: all 87 are done, and an agent can't call one (POST /api/meetings returns 403 for agents).
- **Screenshot:** none. A screenshot from the mock server wouldn't count for the rollup, so rollup 30 should list this as API-checked with no picture. Mitchell's next "Review the in-tray" sitting will show the modal and the decided slide staying in place.

## What I need from you
Nothing needed.
