---
id: "dc_rdr0aqd9ae"
type: "report"
state: "building"
title: "Review deck design filed (dc_y7a8g257of): assembled in code from in-tray data (0 tokens, <1 s); fresh pictures cost 1–2.5 min each, so they're drafted at rollup/proposal time; KR draft and ~700k-token 4-step plan"
authorId: "ag_odrq1n6z0d"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_y7a8g257of","dc_wgy9v6hdkx","dc_tcoy1plt2r","dc_p68jzo79xq","dc_nhd0maw3f5"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Design accepted. I write the KR under the Trust objective and propose the ~700k grant from dc_y7a8g257of in this session; the migration in step 3 (Meeting.deck) is flagged in the proposal note for Mitchell."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T20:37:01.638Z"
sessionId: "se_joz0mkivyq"
assignmentId: "as_rj8d98dauk"
costUsd: 0.9786716999999999
tokens: 48934
turns: 24
createdAt: "2026-10-28T20:08:41.217Z"
updatedAt: "2026-10-28T20:37:01.638Z"
---
## What I did
I read the 1:1 notes [dc_wgy9v6hdkx](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-pix-notes-y9v6hdkx.md), Lena's meeting-kinds article [dc_tcoy1plt2r](../../article/2026-10/2026-10-27-meeting-kinds-today-oy1plt2r.md), the demo-media skill [dc_p68jzo79xq](../../skill/2026-10/2026-10-27-demo-media-8jzo79xq.md), Town blockers [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md) and the in-tray code (domain.ts `townHallIntray`, web Places.tsx GrantRow, GrantPanel History, RollupCards and parseRollup from 689761f). I timed a real screenshot pipeline on my desk against the live town. Then I filed the design **[Design: the review deck](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md)** in the Workshop cabinet (read-only, no code changed, no PR).

## Findings
- **Main design call: the review deck is computed, not drafted.** Every field a slide needs already exists as data: rollup items (what it is, what you'd see, picture, your call), grants with `history[]`, and key-result stoplights. So `GET /api/review-deck` builds the deck when it is opened, in under 1 s for 0 tokens. Agents write a slide's content only when a field is missing, and they do it at rollup or proposal time. As part of that, `propose_grant` gains an optional `picture` and `whatYoudSee`.
- **Slide order, blocking-most first:** held checkpoints, then blocked buildings, then items that parked work waits on (ranked by count of `waitFor`/`resumeWhen {decision}`), then proposals oldest first, then rollups with a real "Your call", then closed-as-done KRs. Rollups whose calls are all "None" collapse into one "For the record" slide with Approve all.
- **On each slide:** the item's age and waiter count, the four fields, the existing decision buttons (GrantRow and rollup approve/reply/Talk to author), and a one-line history (last human entry in GrantView.history, the building's previous rollup decisionNote, or the `mt_` decision it came from).
- **Measured on my desk at 20:05Z:**
  - Playwright setup: 2 s.
  - Screenshot capture: 7.3, 13.9 and 21.5 s; a doc-panel crop took 48.0 s.
  - Upload: 0.1 s.
  - Agent work around one capture: about 4 turns at about 1.6k adjusted tokens per turn.
  - So one fresh picture costs about 1–2.5 min and 5–10k tokens, and a 5-slide all-fresh deck about 6–12 min and 30–50k tokens.
  - **Verdict:** generate pictures ahead of time, assemble the deck live, and never generate during the meeting.
- **Live in-tray now:** 1 rollup and 3 proposals, so today's deck would be 5 slides. That matches about 4.2 decisions per sitting over 7 days (Town blockers).
- **Deck doc type:** `deck`, with markdown slides split on `---`, media per slide, a `Notes:` line for the presenter, ← → keys and a `#/doc/<id>/<n>` URL. A presenter view in meetings via a `Meeting.deck {docId, slide}` column (needs a migration), and "— slide n" lines in the transcript.
- **Meeting mode:** Lena's Call-a-meeting form gets Mode: Chat or Presentation with chat. The preset "Review the in-tray" uses the review deck.
- **KR draft (Trust ob_s7jsvvoe5p):** "Mitchell reviews the Town Hall in-tray as one review deck: slide 1 shows the state of the town and each later slide is one pending decision (blocking-most first) with what it is, what you'd see, a picture, your call, a one-line history and its decision buttons, and at least one in-tray sitting is held as a Presentation meeting."
  - **How to check:** Review as deck in the Town Hall in-tray opens slides with ← →. Deciding on a slide advances to the next. The event log shows decision events with `payload.deckSlide`, and one "Review the in-tray" meeting's notes contain "— slide n" lines.
- **Build plan, about 700k adjusted tokens (620–880k):**
  1. Deck type and slide viewer: 150–220k.
  2. Review deck endpoint and button: 250–350k.
  3. Presentation meeting mode: 180–250k (excludes Lena's form, which is a separate 300–450k).
  4. Live check: 40–60k.
  - Stop condition: the check passes live, or step 3 is dropped if the async deck alone brings the p90 wait under 4 h.
- **Forks step 2 test:** about 17 turns. I estimate about 40–60k adjusted tokens from turn count; I did not measure it.
  - Friction: the town-hall in-tray URL is `/api/buildings/town-hall/intray`, not `/api/intray/…` (one wasted call).
  - The demo-media skill's scripts have to be retyped by hand on each desk; there is no download.
  - A redeploy is waiting on this session, so I stopped without writing a topic page. The plan is in this report and in [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md).
- I didn't push anything, so no commit needs to go live from this session.

## What I need from you
Nothing needed. Pix: set the KR above and propose the grant from [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md).
