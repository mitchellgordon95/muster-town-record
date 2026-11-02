---
id: "dc_6y7huetn7t"
type: "report"
state: "building"
title: "Presentation fixes on main 75d3110 (modal, pinned deck with decided slides, picture placeholder); redeploy queued, live check next"
authorId: "ag_y2kddf86jx"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. All three sitting fixes (modal, pinned deck with decided slides, picture placeholder) are on main at 75d3110 with tests; the parked continuation as_1nggypfpum live-checks once 75d3110 deploys. If no human-called presentation is running, check the ?meeting= API and the picture fix on the live deck, and say the modal screenshot still needs Mitchell's next sitting."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T15:54:04.763Z"
sessionId: "se_jkram7cy9h"
assignmentId: "as_risa9dywkv"
costUsd: 2.7011110000000005
tokens: 135056
turns: 51
createdAt: "2026-10-29T15:53:21.089Z"
updatedAt: "2026-10-29T15:54:04.763Z"
---
## What I did
I fixed all three items from Mitchell's sitting mt_xywhisvdcm (decision 7) in one commit, 1f8fa8c. It's merged to main as 75d3110 (PR https://github.com/mitchellgordon95/muster-town/pull/77), and I queued a redeploy at about 15:55Z. Tests and typechecks pass: core review-deck (8 tests, 2 new) and presentation (5), server review-deck (2), web meetingSlide (3, 1 new) and reviewDeck (3); tsc is clean on schema/core/server/web/runtime; check:docs passes. docs/meetings.md §10 and the topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md) are updated.

## Findings
- **1. The slides open in a modal.** MeetingSlide now shows the slide in a box centred over the map, to the left of the side panel. The chat stays in the panel, which shows one line: "Presenting: … · slide n of N · Hide/Show slides". The map stays clickable around the box. On screens 760 px wide or less, where the panel takes the whole width, the slide stays above the chat. I checked it headless on the mock dev server only: the box sits centred, the chat bar is in the panel, there were no page errors, and the presenter controls are inside the modal.
- **2. A decided slide stays in place.** When a review-deck meeting goes live, and again on every slide move, the meeting saves its slide list in `Meeting.deck.pinned`. This is a JSON field on the existing column, so no migration. `GET /api/review-deck?meeting=<id>` (core `presentedReviewDeck`) returns the slides in that saved order:
  - A slide whose item is still in the in-tray is refreshed from the live in-tray.
  - A slide whose item was decided stays at its number, starts with "_Decided: cut_" (or rejected, funded, approved, "key result marked met"), and its buttons are replaced by "Decided: x. Move on with →."
  - New in-tray items are added at the end.
  - "— slide n" transcript lines and `payload.deckSlide` are unchanged.
  - A test covers it: reject on slide k, and the keys and numbers stay the same, slide k is marked "rejected", and a new rollup is appended.
- **3. Cause of the broken picture.** The checkpoint slide takes its picture from the grant's findings docs. For gr_jh0lu0w6yj, the first image in its findings doc [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md) is a literal example, `![alt](/api/media/mf_….png)`. The slide builder now only accepts `/api/media/mf_…` links whose media actually exists, and checks every image in each doc, not just the first. With no real image the slide reads "_no picture_". A test covers it.
- **Live-checked: none yet.** All three wait for 75d3110 to be live. I parked on that deploy; the continuation will live-check and take the cropped modal screenshot for rollup 30. One limit: an agent can't call a meeting, so if no live presentation is running, the modal screenshot needs a human-called meeting. Otherwise I can only check the `?meeting=` API on mt_xywhisvdcm (its deck has no pin, so it returns the live deck) and the picture fix on the live deck.

## What I need from you
Nothing needed.
