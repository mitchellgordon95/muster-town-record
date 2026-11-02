---
id: "dc_jar113azkv"
type: "report"
state: "building"
title: "Meeting kinds today (dc_tcoy1plt2r): retro and planning are labels only; one \"Call a meeting\" form with presets proposed"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_tcoy1plt2r","dc_evzrmyl3pp","mt_6830h8x5qk"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Table and proposal are what decision 4 asked for. Step 2 waits for Mitchell's answer on dc_tcoy1plt2r; it goes in the rollup. Your queued visitor-agent review (as_1vn3yowh6n) is next."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:51:18.539Z"
sessionId: "se_98gf6bg8yh"
assignmentId: "as_sludby0v5i"
costUsd: 1.1371766
tokens: 52367
turns: 24
createdAt: "2026-10-27T17:49:25.440Z"
updatedAt: "2026-10-27T17:51:18.539Z"
---
## What I did
Read the meeting code on main at 4be312e (schema, core/meetings.ts, prompts.ts, runtime/meetings.ts, scheduler, both web call-meeting forms) and the live GET /api/meetings. Filed the article [Meeting kinds today](../../article/2026-10/2026-10-27-meeting-kinds-today-oy1plt2r.md) in the Workshop filing cabinet: a table with one row per kind, plus a one-page proposal. No code changed and nothing to deploy. The redeploy that is waiting will run on whatever is already on main.

## Findings
- The town has **5 kinds**: standup, retro, planning, town-hall, one-on-one. There is no "ad hoc" kind; an ad hoc meeting is a standup with attendees picked by hand.
- **retro and planning are only labels.** No code branches on them. They invite the same people, ask for the same Did/Next/Need summary (the prompt even says "at a standup") and give the facilitator the same prompt. Live: 0 of 59 meetings are retro or planning (27 standup, 12 town hall, 20 1:1).
- **Where a meeting is called decides how it behaves, not its kind.** Calling it in a lab building or in the Town Hall sets the default attendees, the facilitator, which in-tray the facilitator sees, and where the notes are filed (the building's cabinet or the library). The town-hall kind adds one thing of its own: the facilitator opens with "Decisions needed from the humans". Quirk: Building → Meetings lets you pick town-hall inside a lab building, or standup in the Town Hall, which mixes the two.
- **The 1:1 works differently from the rest.** It has no summaries and no facilitation session. Only the manager and the human speak, and only the human can end it.
- **Agenda:** the schema and API already accept an `agenda`, and it already reaches the facilitator, the summaries and the notes. But no web form has a box for it, so 0 of 59 meetings have one. No building has a meeting schedule set, so no meeting ever starts by itself.
- **Proposal:** one "Call a meeting" form with these fields: preset, title, agenda items, attendees, what each attendee brings (status update / nothing / custom text) and an "ask the humans for decisions" checkbox. The presets are Standup, Town hall, Review the in-tray (your ask from this town hall), Retro, Planning and Blank; each pre-fills those fields and leaves them editable. The 1:1 stays its own button. Step 2 needs migration 044 (two new columns), changes to core and prompts (the opener follows the checkbox instead of the kind; the summary prompt uses what attendees bring), a runtime change (with "nothing", skip the 3-minute summary round), and one web form replacing the two that exist now. Estimate: 2 build sessions plus a live check, about 300–450k adjusted tokens (±50%).

## What I need from you
Mitchell: read the table in [dc_tcoy1plt2r](../../article/2026-10/2026-10-27-meeting-kinds-today-oy1plt2r.md) and say whether step 2 should build the form as proposed (or which presets and fields to change).
