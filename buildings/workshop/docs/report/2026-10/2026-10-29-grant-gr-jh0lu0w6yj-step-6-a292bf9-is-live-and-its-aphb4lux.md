---
id: "dc_w3aphb4lux"
type: "report"
state: "building"
title: "Grant gr_jh0lu0w6yj step 6: a292bf9 is live and its routes check out, but the sitting needs a human (agents can't call a meeting)"
authorId: "ag_ywszk292se"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "pivot"
decision: "approve"
decisionNote: "Approved. Right call not to force a sitting: agents can't call a meeting (403 meeting.facilitate), so steps 2-4 are Mitchell's 3-minute sitting in rollup 30's Your call. No further fork on step 6; I close gr_jh0lu0w6yj on the sitting's meeting id."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T05:37:40.003Z"
sessionId: "se_ta0pm5ph7w"
assignmentId: "as_7hhtyvjs6h"
costUsd: 1.0254458
tokens: 51272
turns: 27
createdAt: "2026-10-29T05:37:25.964Z"
updatedAt: "2026-10-29T05:37:40.003Z"
---
## What I did
- Confirmed that a292bf9 is live (health commit a292bf9, 05:35Z).
- Tried to call the "Review the in-tray" meeting (review deck, me as the only attendee). It was refused with 403: "you need the meeting.facilitate permission here".
- Ran the checks that need no meeting: the present route, the review deck, and the web bundle.
- Rewrote the topic pages [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md) (meetings) and [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) (panels/in-tray).
- Spent about 30k tokens. I made no code changes, opened no PR, and left no meeting open.

## Findings
- **The sitting could not be run by an agent.** `POST /api/meetings` needs meeting.facilitate or building.review, and there is no verb for creating a meeting. Presenting needs the facilitator or a human. So no fork (and no manager session through tools) can run steps 2 and 4 of this assignment. A human has to call the meeting.
- **Present route is live** (`POST /api/meetings/:id/present`):
  - unknown meeting → 404
  - done meeting mt_auczm6f1j1 → 409 "Meeting is done; you can present only while it is live."
  - The web bundle has "Presentation with chat" (Call-a-meeting Mode) and "Present in".
- **Review deck is live** (`GET /api/review-deck`, 05:40Z). The in-tray list has 8 items (4 reports + 4 grants), which become 10 slides:
  - Slide 1, "State of the town": Bank 11.86M left; spend by lane; "8 decisions below, oldest waiting 11.9 h"; a light per building.
  - Slides 2-10 cover every item: a held checkpoint, 2 proposals, 4 rollup items, 1 closed-as-done, and "For the record".
  - History lines:
    - slide 9: "Mitchell funded 1.8 h ago"
    - slide 2: "Town held 40 min ago: …"
    - slides 5-8: "Mitchell approved the previous rollup …"
    - slides 3-4 (proposals) have none, because no human has decided on them before.
  - Same layout as e74ae79, so the picture mf_fyh4eibt3d still matches. I took no new screenshot.
- **Not yet seen live:**
  - the slide synced above the chat
  - the "— X is presenting … (N slides)" and "— slide 2: …" lines
  - the facilitator's "Presenting: …, slide n of N" material and the `slide` in its status
  - "(on slide n)" in a meeting's decisions

  Unit tests cover all four (core presentation 5/5, server review-deck 2/2, web meetingSlide 2/2).
- **Grant cost record:** step 5 ~150k (Pix 2); step 6 ~30k (Pix 1); 0 lost sessions. The grant is not ready to close: the KR's "deciding on a slide advances" part has never been seen live.
- **Suggestion:** the manager should not queue another fork for this. Steps 2 and 4 together are a single human sitting (below), and the grant can be closed on its result.

## What I need from you
Mitchell (rollup 30 Your call), one sitting of about 3 minutes:
1. In the Town Hall, open Call a meeting, pick the "Review the in-tray" preset and start it.
2. Check that the slide sits above the chat, then press → once. The transcript should show "— Mitchell is presenting … (10 slides)" and "— slide 2: …".
3. Decide one item from its slide, and check that the meeting's Decisions show "(on slide n)".
4. End the meeting.

Then the manager closes gr_jh0lu0w6yj with that meeting id as the evidence.
