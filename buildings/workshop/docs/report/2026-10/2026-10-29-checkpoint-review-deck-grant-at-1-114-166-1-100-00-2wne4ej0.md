---
id: "dc_9f2wne4ej0"
type: "report"
state: "building"
title: "Checkpoint: review-deck grant at 1,114,166 / 1,100,000 — all six steps live at a292bf9, key result on-track; the last evidence is your 3-minute \"Review the in-tray\" sitting"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_fv4li1gq7g","dc_eyf77x16kx","dc_0wia0ldzlr","dc_xnoma8l583","dc_nyw7x6x8q0","dc_byeupnc8iq","dc_mra1k8qled","dc_ppmg2cdkhy","dc_71toiuzway","dc_o5iz67jmoz","dc_yv875nf3z3","dc_t83tp99zda","dc_w3aphb4lux"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T15:39:59.319Z"
sessionId: "se_gvzk413z2s"
assignmentId: "as_tfa7thuoc6"
costUsd: 2.6272024
tokens: 52544
turns: 15
createdAt: "2026-10-29T05:41:37.965Z"
updatedAt: "2026-10-29T15:39:59.319Z"
---
Live commit a292bf9 (GET /api/health, 05:38Z). This is the checkpoint for the review-deck grant gr_jh0lu0w6yj: it crossed 100% at 05:37Z. Its code is all live; what is missing is one human-called meeting.

## Shipped

**1. The in-tray reviews as one deck, and a meeting can present it (grant steps 3-6)**
**What it is:** A "deck" document type with a slide viewer (arrow keys, slide in the URL); GET /api/review-deck builds the in-tray into slides in code at 0 tokens (slide 1 the state of the town, then one slide per pending item, blocking-most first, each with what it is, what you'd see, a picture, your call, a one-line history and its decision buttons); a meeting Mode "Presentation with chat" that syncs the slide above the chat and writes "— slide n" lines into the transcript, with a "Review the in-tray" preset. Migration 054 added one nullable column (Meeting.deck), as named in the funded plan. Reports [dc_byeupnc8iq](2026-10-29-grant-step-3-pushed-deck-doc-type-and-slide-viewer-eupnc8iq.md), [dc_71toiuzway](2026-10-29-grant-step-4-pushed-get-api-review-deck-and-review-toiuzway.md), [dc_yv875nf3z3](2026-10-29-review-deck-no-longer-cuts-slide-text-proposal-app-875nf3z3.md), [dc_t83tp99zda](2026-10-29-presentation-with-chat-grant-step-5-on-main-at-a29-3tp99zda.md); live checks [dc_mra1k8qled](2026-10-29-2d8694d-is-live-a-real-deck-doc-dc-z2txaz0ur5-open-a1k8qled.md), [dc_o5iz67jmoz](2026-10-29-grant-step-4-live-at-e74ae79-get-api-review-deck-a-iz67jmoz.md), [dc_w3aphb4lux](2026-10-29-grant-gr-jh0lu0w6yj-step-6-a292bf9-is-live-and-its-aphb4lux.md).
**What you'd see:** Town Hall in-tray → "Review as deck": today 11 slides for 10 pending items (2 held checkpoints, this one among them; 2 proposals; 4 rollup items; 1 closed-as-done; "For the record"), with history lines such as "Mitchell funded 1.8 h ago". Call a meeting → Mode → "Review the in-tray".
![Review as deck in the Town Hall in-tray](/api/media/mf_fyh4eibt3d)
**Your call:** The 3-minute sitting that claims the key result: Town Hall → Call a meeting → "Review the in-tray" preset → start. Check the slide sits above the chat, press → once (transcript: "— Mitchell is presenting … (11 slides)", "— slide 2: …"). Decide one item from its slide and see "(on slide n)" in the meeting's Decisions. End the meeting.

**2. Meetings start from full context, through one Call-a-meeting form (grant steps 1-2)**
**What it is:** Facilitators and attendees load their wiki, prior meeting decisions and FYIs when a meeting starts; one Call-a-meeting form with presets, agenda, what attendees bring and ask-the-humans replaced the Standup form and the old town-hall button (1:1 kept its own). Reports [dc_eyf77x16kx](2026-10-29-grant-step-1-pushed-meeting-sessions-run-on-full-c-f77x16kx.md), [dc_xnoma8l583](2026-10-29-grant-step-2-pushed-one-call-a-meeting-form-with-p-oma8l583.md); live checks [dc_0wia0ldzlr](2026-10-29-e503b55-is-live-health-ci-green-tests-re-run-the-m-ia0ldzlr.md), [dc_nyw7x6x8q0](2026-10-29-d92ef20-is-live-call-a-meeting-form-in-the-web-bun-w7x6x8q0.md).
**What you'd see:** Town Hall → Call a meeting: preset, agenda items, Mode. Otherwise API-only: GET /api/meetings returns brings and askHumans. No picture (the deck picture above is this rollup's one).
**Your call:** None. The sitting in item 1 exercises the form too.

## Decided
- [dc_fv4li1gq7g](2026-10-28-session-ended-without-a-report-grant-gr-jh0lu0w6yj-4li1gq7g.md) → redirect (step 1 session ended without a report, 78,188 tokens lost; step 1 re-queued)
- [dc_eyf77x16kx](2026-10-29-grant-step-1-pushed-meeting-sessions-run-on-full-c-f77x16kx.md) → approve (step 1 on main e503b55)
- [dc_0wia0ldzlr](2026-10-29-e503b55-is-live-health-ci-green-tests-re-run-the-m-ia0ldzlr.md) → approve (e503b55 live)
- [dc_xnoma8l583](2026-10-29-grant-step-2-pushed-one-call-a-meeting-form-with-p-oma8l583.md) → approve (step 2 on main d92ef20, migration 052)
- [dc_nyw7x6x8q0](2026-10-29-d92ef20-is-live-call-a-meeting-form-in-the-web-bun-w7x6x8q0.md) → approve (d92ef20 live)
- [dc_byeupnc8iq](2026-10-29-grant-step-3-pushed-deck-doc-type-and-slide-viewer-eupnc8iq.md) → approve (step 3 on main 2d8694d)
- [dc_mra1k8qled](2026-10-29-2d8694d-is-live-a-real-deck-doc-dc-z2txaz0ur5-open-a1k8qled.md) → approve (2d8694d live: deck [dc_z2txaz0ur5](../../deck/2026-10/2026-10-29-deck-viewer-live-check-gr-jh0lu0w6yj-step-3-txaz0ur5.md) opens on slide 2 by URL)
- [dc_ppmg2cdkhy](2026-10-29-session-ended-without-a-report-grant-gr-jh0lu0w6yj-mg2cdkhy.md) → approve (step 4 session hung at the desk, 0 tokens; step 4 re-queued)
- [dc_71toiuzway](2026-10-29-grant-step-4-pushed-get-api-review-deck-and-review-toiuzway.md) → approve (step 4 on main e74ae79)
- [dc_o5iz67jmoz](2026-10-29-grant-step-4-live-at-e74ae79-get-api-review-deck-a-iz67jmoz.md) → approve (e74ae79 live, screenshot mf_fyh4eibt3d)
- [dc_yv875nf3z3](2026-10-29-review-deck-no-longer-cuts-slide-text-proposal-app-875nf3z3.md) → approve (no-truncation fix d402784)
- [dc_t83tp99zda](2026-10-29-presentation-with-chat-grant-step-5-on-main-at-a29-3tp99zda.md) → approve (step 5 on main a292bf9, migration 054)
- [dc_w3aphb4lux](2026-10-29-grant-gr-jh0lu0w6yj-step-6-a292bf9-is-live-and-its-aphb4lux.md) → approve (a292bf9 live; the sitting needs a human: agents get 403 on POST /api/meetings)

## Key results

| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_2qg0ayfs1j The Town Hall in-tray reviews as one deck; one in-tray sitting held as a Presentation meeting | gr_jh0lu0w6yj | on-track (checkpoint, this report) | 1,114,166 / 1,100,000 (101%) |
| kr_vyrhhiyotb The Bank counts adjusted output tokens | gr_iq5m7dug56 | on-track | 1,640,037 / 1,666,667 |
| kr_6f9c200vsx A member who is not an admin or manager funds a key result end to end | gr_tvt32g9xly | not-started | 271,900 / 300,000 |

Today's spend by lane: exploration 169,555 / 828,571 tokens; directed 767,197 tokens.

**How to check kr_2qg0ayfs1j:** Town Hall in-tray → "Review as deck" opens slides with ← →, one per pending item, a history line on any grant with a prior decision; deciding on a slide advances. Event log: in-tray decisions carry payload.deckSlide; one "Review the in-tray" meeting's notes contain "— slide n" lines.

**What the testing plan showed (checked against the live town at 06:05Z):**
1. Full context at meeting start: live since e503b55 (00:42Z); 10 meetings have run on it since. Verified by unit tests and the bundle, not by reading a session log (none of the 10 was opened by a fork).
2. One Call-a-meeting form with presets, agenda, mode: live in the web bundle and the API (d92ef20). No meeting has yet been called through the form with agenda items, so "agenda appears in its notes" is unit-tested only.
3. A deck plays in the side panel: holds live ([dc_z2txaz0ur5](../../deck/2026-10/2026-10-29-deck-viewer-live-check-gr-jh0lu0w6yj-step-3-txaz0ur5.md) opens on slide 2 by URL, pictures per slide, no truncated text after d402784).
4. Review as deck with decision buttons, blocking-most first, history lines: holds live (11 slides today). "A decision carries payload.deckSlide": 0 such events in the log from id 43001 (10-28 21:17Z) to 50134, because no human has decided from a slide yet.
5. One sitting as a Presentation meeting: not held. POST /api/meetings answers 403 meeting.facilitate for agents, so no fork can produce it.

**Spend by step (13 sessions, sum equals the ledger):** step 1 148,792 (78,188 lost in a session that ended without a report); step 2 140,336; step 3 189,187; step 4 334,222 (one 0-token lost session, plus the no-truncation fix); step 5 250,357; step 6 51,272. Overrun 14,166 tokens (1.3%).

**Whether to continue:** No more fork work is planned; every remaining line of evidence comes from your sitting. After it, I close the grant with the meeting id and the deckSlide event as evidence, and you mark the key result met.

## Needs from Mitchell
1. Hold the 3-minute "Review the in-tray" sitting (item 1's Your call). Then either continue this grant with a top-up of about 40,000 tokens, so the close session (charged to the grant) can file the close report and claim the key result, or cut it after the sitting and mark the key result met from the in-tray yourself. Why: all six steps are live and the only missing evidence is a meeting agents cannot call.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_fenzvxqy2c](../../../../../town-hall/outbox/2026-10/2026-10-29-flip-prod-settings-budget-mode-to-forks-prod-s-ste-nzvxqy2c.md)), 0 rollups._
