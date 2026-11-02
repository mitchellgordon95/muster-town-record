---
id: "dc_y7a8g257of"
type: "article"
state: "building"
title: "Design: the review deck (in-tray review as a presentation with chat)"
authorId: "ag_odrq1n6z0d"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_wgy9v6hdkx","dc_tcoy1plt2r","dc_p68jzo79xq","dc_nhd0maw3f5","dc_6tsgcif8r1"],"urls":[]}
tags: ["design","meetings","in-tray","review-deck"]
createdAt: "2026-10-28T20:08:21.443Z"
updatedAt: "2026-10-28T20:08:21.443Z"
---
# Design: the review deck

Decision 2 of Mitchell's 1:1 mt_vcn0e66r1t (notes [dc_wgy9v6hdkx](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-pix-notes-y9v6hdkx.md)). Read from main at 54b4d02 (live b501e92). This is a design only; no code was changed.

**The problem, measured** (Town blockers [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md), 7 days to 2026-10-28): 109 human decisions were made in 26 sittings, about 4.2 per sitting. Grant proposals waited a median of 1.2 h, p90 13.8 h. Rollups waited a median of 0.9 h, p90 10.4 h. Managers decide resident reports in a median of 2 min. The cost is not the decisions themselves. It is opening each item and rebuilding its context. Live now (20:05Z): 1 rollup and 3 proposals pending, so today's deck would be 5 slides.

**The core idea: assemble the deck in code, don't write it.** Every field a slide needs already exists as data:
- Rollup items carry what it is, what you'd see, a picture and your call (parseRollup, 689761f).
- Grants carry objective, ask, `history[]` and spend.
- Key results carry stoplights.

So the review deck is a view the server computes when it is opened: zero tokens, under 1 s, always current. Agents write prose only where a field is missing, and they do it ahead of time, not during the meeting (see §3).

## 1. Deck doc type

- **Schema:** `DocType` adds `"deck"`. The body is markdown and slides are split on a line `---`. The first slide's `#` heading is the deck title. A slide shows its pictures as usual (`![alt](/api/media/mf_….png)` or `.webm`; MediaThumb already renders both). An optional last line `Notes: …` is presenter-only text. No migration: the doc type is a string column. Check `DocType` users, the zod enum and the `write` description.
- **Side panel:** DocView renders a deck as one slide at a time: the slide fills the panel, a picture is scaled to fit, and a `3 / 7` counter and a dot strip sit at the bottom. Keys: ← → (also PgUp/PgDn and space) move between slides, Home/End jump, `f` goes fullscreen with the panel at the maximum width (the panel-resize code from 869f76d). The URL is `#/doc/<id>/<n>`, so a slide can be linked and the browser's back button works. The no-truncation rule ([dc_w6e1vpbkuf](../../wiki/2026-10/2026-10-28-workshop-standing-rules-e1vpbkuf.md)) holds: long slide text scrolls inside the slide and is never clipped.
- **Presenter view in a meeting:** `Meeting.deck = {docId, slide}` is a new JSON column (one small migration; check the highest number on main). Whoever started the meeting, or the human, presses Present on a deck. Everyone's meeting panel then shows the current slide above the chat, kept in sync over the existing meeting websocket updates. The presenter alone sees the Notes line and the next slide's title. When the presenter moves slides, the server appends a system line to the transcript ("— slide 3: Prod rollup #15"), so the notes record which slide each remark was about.

## 2. The review deck (town-wide, assembled)

`GET /api/review-deck` builds it from `townHallIntray()` (domain.ts) plus key results. It is rendered by the same slide viewer, but it is a computed view, not a stored doc. Opening it from the Town Hall in-tray header button **Review as deck** costs nothing.

**Slide 1: state of the town.** Bank balance and spend today against the allowance (from /api/health budgets); one row per building with its key results as stoplights (the existing `Stoplight` and `KeyResultsView`); "N decisions below, oldest waiting X h". Any flags Mitchell planted that are still pending after 2 h appear here as one line ("your flag in Prod is still waiting, 3 h"), not as slides: flags belong to managers.

**One slide per decision, in this order** (what blocks the most work comes first):
1. Checkpoint grants held. The building's grant work is stopped until a human decides.
2. Blocked buildings (`blocked[]`).
3. Items that work is parked on. These are ranked by `waiters`: assignments with `waitFor {decision: <id>}` plus continuations parked with `resumeWhen {decision}`, counted from the assignments table.
4. Grant proposals, oldest first.
5. Rollups whose items have a "Your call" other than None, oldest first.
6. Grants closed as done whose key result needs met or missed.

Rollups whose every call is "None" collapse into a single closing slide, "For the record (no decision): Prod #15, Bank #9", with one **Approve all** button.

**What each slide shows** (age and waiter count at the top, e.g. "Waiting 4.1 h · 2 assignments parked on this"):
- **What it is**, **What you'd see**, **Picture**, **Your call.** A rollup gives one slide per Shipped item with a non-None call, taken straight from parseRollup. A proposal maps objective → what it is, the testing plan's howToCheck → what you'd see, ask and stop condition → your call, and the picture is the first media in its findings docs if there is one.
- **The decision buttons, inline.** These are the existing components, not new endpoints: `GrantRow`'s fund / counter / reject / continue / adjust / cut, and the rollup's approve / reply / Talk to <author> (1:1 decision mt_uf1bwd3exq). Deciding moves to the next slide on its own.
- **One line of history**, so Mitchell does not have to rebuild context:
  - For a grant: its last human entry in `GrantView.history` ("You countered 2 d ago: 'halve the ask'").
  - For a rollup: the same building's previous rollup decision and its `decisionNote`.
  - For any item whose provenance names a meeting with him (`mt_…`): that meeting's decision text ("You asked for this in 1:1 mt_vcn0e66r1t: …").

  Each source is one query; if none applies, the line is left out.

Illustration of what slide 1 would draw on (the live Bank panel, captured during this design's timing test): ![Bank panel (review-deck timing test)](/api/media/mf_rrewqy3t6x.png)

## 3. Presentation meeting mode, and who drafts

**In Lena's Call-a-meeting form** ([dc_tcoy1plt2r](2026-10-27-meeting-kinds-today-oy1plt2r.md)), add a field **Mode: Chat | Presentation with chat**. The preset "Review the in-tray" pre-fills it as Presentation, with the review deck as its deck, attendees nothing to bring (straight to discussing), and the decisions opener on. Any other preset can pick Presentation and attach any deck doc. The facilitator's prompt gets the current slide; when the human types about a slide, the facilitator answers or @mentions that building's manager (the existing ≤5 read/search replies). A decision made from a slide is recorded as a normal meeting decision plus the in-tray decision event, with `payload.deckSlide`.

**Who drafts, and when.** Because the review deck is assembled in code, nobody drafts it. What can be missing is a slide's *content*:
- Rollups: the manager's fork already writes the four fields and the picture at rollup time (the decision-1 format, now enforced by submit_report). Nothing more is needed.
- Proposals: today they have no picture and no "what you'd see". Have `propose_grant` take an optional `picture` (mf_…) and a `whatYoudSee` line, so the manager writes them when proposing. That is the same time the rollup is written, so no extra session.
- No Town Hall job before the meeting. A slide with a missing field still renders and shows "no picture".

**Measured slide-generation time** (my desk, 2026-10-28 20:05Z, demo-media skill [dc_p68jzo79xq](../../skill/2026-10/2026-10-27-demo-media-8jzo79xq.md), live town):

| Step | Wall clock |
|---|---|
| One-time setup (`npm i playwright-core`, cached) | 2 s |
| `capture.mjs shot` of the Bank panel, 3 runs | 21.5 s, 7.3 s, 13.9 s |
| Doc panel shot with `SELECTOR=.panel` | 48.0 s |
| `upload.sh` | 0.1 s |

The agent work around a capture is about 4 turns: choose the view, capture, look at the image to check the crop, upload. My Workshop sessions average about 1.6k adjusted tokens per turn (as_nzxi6986km: 22,557 tokens over 14 turns). That gives:
- **One fresh picture:** about 1–2.5 min wall clock and 5–10k adjusted tokens. This matches the skill's "≈2 min".
- **A typical 5-item deck where every picture is fresh:** about 6–12 min and 30–50k tokens.
- **Assembly from data that already exists:** under 1 s and 0 tokens.

**Verdict:** pictures are drafted ahead, at rollup or proposal time, by the author who already has the context. The deck itself is assembled live. Never generate pictures inside the meeting: it would add 1–2 min per slide while Mitchell watches.

## 4. After the rollup format is the default

Each rollup Shipped item becomes one slide, with no transformation: `RollupItem {title, whatItIs, whatYoudSee, pictures, yourCall}` is already the slide's shape. RollupCard (web) and the slide share that component. "Decided" and "Key results" from a rollup are not slides: key results feed slide 1, and Decided is shown only in the history line. Needs from Mitchell items (at most 2, with in-tray duplicates rejected by as_m96b70d021) each become a slide in group 3 with a reply box. A rollup that doesn't parse (an old format) becomes one slide showing its markdown with the plain approve button.

## How leads with many projects run this (Mitchell's question)

What staff reviews in large companies have in common, applied here:
- **A pre-read before the meeting.** The deck is available as soon as the in-tray changes, so Mitchell can decide most slides on his own time (async decisions from the deck).
- **The meeting covers only what is left, plus questions.** It is not a tour of every project.
- **A decisions-needed list ordered by what blocks most.** That is §2's ordering.
- **Explicit "no decision needed" items batched at the end.**

Grants are already gated funding with checkpoints, so I'd leave the sprint rhythm alone. Expected effect: one presentation sitting a day, with the p90 wait falling from about 10–14 h to roughly the gap between async looks.

## 5. Key result draft and build plan

**KR (Trust objective ob_s7jsvvoe5p):** "Mitchell reviews the Town Hall in-tray as one review deck: slide 1 shows the state of the town and each later slide is one pending decision (blocking-most first) with what it is, what you'd see, a picture, your call, a one-line history and its decision buttons, and at least one in-tray sitting is held as a Presentation meeting."

**How to check:** In the Town Hall in-tray, Review as deck opens a slide view with ← → navigation, one slide per pending item, and a history line on any grant with a prior decision. Deciding on a slide moves to the next one. The event log shows in-tray decision events with `payload.deckSlide`, and the meeting notes of one "Review the in-tray" meeting show "— slide n" lines.

**Build plan** (Workshop queue, straight to main, redeploy and a parked live check after each step):

| Step | What | Adjusted tokens (estimate) |
|---|---|---|
| 1 | Deck doc type and slide viewer: DocType `deck`, DocView slide mode, keys, `#/doc/<id>/<n>`, the Notes line, web tests | 150–220k |
| 2 | Review deck: `GET /api/review-deck` (ordering, waiter counts, history line, proposal mapping), Review as deck button reusing GrantRow and rollup decision buttons, closing "For the record" slide, `propose_grant` gains `picture` and `whatYoudSee`; core and web tests | 250–350k |
| 3 | Presentation mode: `Meeting.deck` column (migration), Present button, synced slide over the meeting websocket, presenter notes, "— slide n" transcript lines, `deckSlide` on decisions. Depends on Lena's Call-a-meeting form (her step 2, about 300–450k, decided separately); without it, step 3 adds the mode to today's CallMeeting only | 180–250k |
| 4 | Live check: one real deck sitting with Mitchell, screenshots, then the KR is claimed | 40–60k |

**Grant ask: about 700k adjusted tokens** (range 620–880k, ±25%; the web slide view is the least certain part). This excludes Lena's meeting form. Stop condition: the KR check passes live, or step 2 shows the async deck alone brings the p90 under 4 h, in which case step 3 is dropped.

