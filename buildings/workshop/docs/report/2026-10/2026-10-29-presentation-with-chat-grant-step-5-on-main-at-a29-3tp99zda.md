---
id: "dc_t83tp99zda"
type: "report"
state: "building"
title: "Presentation with chat (grant step 5) on main at a292bf9, redeploy queued"
authorId: "ag_23eugj6n6h"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 5 landed on main (a292bf9) with tests; step 6 (live check, one real sitting, claim the KR) queued on the deploy."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T05:33:57.117Z"
sessionId: "se_dzqnmz8h3a"
assignmentId: "as_q1j3skdi09"
costUsd: 5.007145999999999
tokens: 250357
turns: 108
createdAt: "2026-10-29T05:33:43.043Z"
updatedAt: "2026-10-29T05:33:57.117Z"
---
## What I did
Built grant gr_jh0lu0w6yj step 5 from design [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md) (§1 presenter view and §3). Committed straight to main: 57720fc, then a292bf9 (rebased twice onto other work that landed meanwhile). Queued a redeploy. **a292bf9 should be live after it.** It has not been checked live yet; that is step 6. I didn't open a PR because Workshop rules say to commit straight to main. Note that this adds migration 054 (one nullable TEXT column), which the design and this assignment specified.

## Findings
- **Deck column:** `Meeting.deck = {docId, slide, presenterId}`, added in migration `054_meeting_deck.sql`. `docId` is either a deck doc or the literal `review-deck` (schema `REVIEW_DECK_ID`). A chat meeting has null.
- **Present:** `POST /api/meetings/:id/present {docId|null, slide}` calls core `presentSlide`.
  - Who can present: the facilitator, anyone with meeting.facilitate, or any signed-in human. It only works while the meeting is collecting or discussing.
  - Each slide move posts a system line `— slide n: <title>`. A new deck first posts `— X is presenting "…" (N slides)`. Repeating the same slide posts nothing. Each move also fires a `meeting.slide` event.
  - Sending `docId: null` stops the presentation.
- **Synced slide (web):** `panels/MeetingSlide.tsx` shows the slide above the transcript in every attendee's meeting panel.
  - It stays in sync because the meeting row changes on each move, and that row already goes out over the meeting websocket.
  - ← → (when the slide has focus) or the arrow buttons move it for everyone.
  - Only the presenter sees the Notes line and "Next: <title>". The presenter is whoever moved the slide last, or whoever called the meeting.
  - "Present in <meeting>" buttons appear on deck docs (DeckView) and on Review as deck while a meeting is live.
- **Call-a-meeting form:** it now has a Mode field: Chat, Presentation with the review deck, or Presentation with a deck doc id. The "Review the in-tray" preset pre-fills the review deck, together with its existing "nothing to bring" and decisions opener.
- **Facilitator:** `facilitateMaterial` now opens with "Presenting: …, slide n of N" plus the whole slide text and its notes. The `meeting` status and listen actions both return `slide`.
- **Decisions from a slide:** on the review deck, the slide's own buttons send `meetingId` along with the existing `deckSlide`. The grant-decide, reply and archive routes then also record a meeting decision, e.g. `Mitchell funded gr_… "…" (on slide 4)`, via core `recordSlideDecision` (a `meeting.decisions` event with payload.deckSlide). The in-tray event still carries `payload.deckSlide` as before.
- **Tests and checks:**
  - New tests: core `test/presentation.test.ts` 5/5; server `test/review-deck.test.ts` 2/2 (covers the present route, the 401 for guests, and a decision with meetingId); web `test/meetingSlide.test.tsx` 2/2.
  - Existing suites still pass: the whole web suite (123/123), the core meetings/form/prompts/review-deck/reply/grants/export/verbs tests, and runtime `meetings-chat-scheduler` 12/12.
  - `tsc --noEmit` is clean for schema, core, server, runtime, web, cli and desk.
  - `check:docs` passes. `knip` (the dead-code check) isn't installed on the desk, so that check did not run.
- **Docs:** docs/meetings.md §10 and docs/log.md are updated. I left docs/manual.md alone: main already sits at 1,896 of its 1,900-word cap (web `manual.test.ts`).
- **For step 6 (live check):**
  1. `GET /api/health` shows a292bf9.
  2. Call a meeting with the "Review the in-tray" preset; the review deck should sit above the chat.
  3. Move to slide 2 and check the "— slide 2: …" line appears.
  4. Decide on a slide and check the meeting's Decisions list "(on slide n)".
- **Spend:** roughly 150k adjusted tokens, against the 250k cap.
- Topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md) is updated.

## What I need from you
Nothing needed.
