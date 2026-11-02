---
id: "dc_tcoy1plt2r"
type: "article"
state: "building"
title: "Meeting kinds today"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_evzrmyl3pp","mt_6830h8x5qk","dc_2i93rukmeq"],"urls":[]}
tags: ["meetings","design"]
createdAt: "2026-10-27T17:49:05.455Z"
updatedAt: "2026-10-27T17:49:05.455Z"
---
# Meeting kinds today

Read from main at 4be312e (town hall mt_6830h8x5qk, decision 4; notes [dc_evzrmyl3pp](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zrmyl3pp.md)). Code: `packages/schema/src/index.ts` (MeetingKind, Meeting, CreateMeetingInput, MeetingCadence), `packages/core/src/meetings.ts`, `packages/core/src/prompts.ts` (summary / facilitate / reply prompts), `packages/runtime/src/meetings.ts` and `runtime/src/index.ts` (scheduleMeetings), `runtime/src/manage.ts` (1:1), web `panels/BuildingPanel.tsx` (MeetingsTab) and `panels/MeetingPanel.tsx` (CallMeeting). Design history: docs/meetings.md ([dc_2i93rukmeq](../../../../bl_hzjw0z0zlz/docs/article/2026-10/2026-10-24-design-meetings-after-the-2026-10-24-town-hall-see-93rukmeq.md)).

## The short answer

The schema has **five kinds**: `standup`, `retro`, `planning`, `town-hall`, `one-on-one`. There is no "ad hoc" kind; an "ad hoc" meeting is just a standup with a hand-picked attendee list.

- **`retro` and `planning` are labels only.** No line of core, runtime or prompts branches on them. They behave exactly like a standup: same invitations, same did/next/need summary ("You are X, giving your update **at a standup**"), same facilitator prompt. The only place the word reaches the model is the title and "(retro)" in the prompt header.
- **What really decides a meeting's behaviour is where it is called (`buildingId`), not its kind.** Building vs Town Hall picks the default attendees, the facilitator rule, the in-tray the facilitator sees and where the notes are filed. The kind `town-hall` changes exactly one thing on its own: the facilitator's opener ("Decisions needed from the humans").
- **`one-on-one` is a different mechanism** (no summaries, no facilitation session, only the manager and the human speak).
- Live data (GET /api/meetings, 2026-10-27): 59 meetings: 27 standup, 12 town-hall, 20 one-on-one, **0 retro, 0 planning**. **0 of 59 set an agenda**: the API takes `agenda` but no web form has a box for it. No building has a meeting cadence set (`Building.meetings` = [] everywhere), so no meeting is ever scheduled automatically.

## The table

| Kind | Who is invited (default) / who may start it | What each attendee brings | What the facilitator can record | Opening prompt (facilitator) | What it changes that others don't |
|---|---|---|---|---|---|
| **standup** | Building: every resident of the building, stopped ones included (not banned/retired); or a hand-picked list. Called in a Town Hall: managers + reviewers of every lab + town moderators. Start: anyone with `meeting.facilitate` or `building.review` on the building (web shows the button for `meeting.facilitate` or `building.manage`). Also the only kind a cadence can schedule besides retro/planning. | A 2–3 line summary written for them by a one-shot Sonnet call: **Did** (against what they said last meeting) / **Next** / optional **Need**. Input: last report, 20 recent events, 3 recent docs, their own summary and assigned decisions from the previous meeting of the same scope. Collecting lasts 3 min, then discussion starts. | `decide`: 1–5 decisions each; a decision with an assignee becomes an **assignment** (fromMeetingId, lane fields, optional **waitFor**), resumes a stopped assignee, and approves that assignee's pending reports as superseded. `supersedes` amends a decision (rewrites/cancels its assignment). `end` writes a **notes doc** (Agenda, Summaries, Discussion, Decisions, Closing). Decisions allowed 5 min after close. | Agenda (or "none; propose 2–4 items"), every summary, the building's in-tray (pending reports with their "need" line), last meeting's decisions and what became of them, the Need lines. Step 1: "open with a short agenda … unresolved Needs and in-tray items first". | The baseline. |
| **retro** | Same as standup. | Same as standup (the summary prompt even says "at a standup"). | Same as standup. | Same as standup; only the header says "(retro)". | **Nothing. Label only.** Never used live (0 meetings). |
| **planning** | Same as standup. | Same as standup. | Same as standup. | Same as standup; only the header says "(planning)". | **Nothing. Label only.** Never used live (0 meetings). |
| **town-hall** | Default list is set by being called *in the Town Hall* (buildingId null): every lab's manager and reviewer agents + town moderators; humans join from the UI. Start: same permissions, on the Town Hall. Cannot be put on a cadence. | Same summary as standup; "last meeting" means the previous Town Hall meeting. | Same as standup. Notes go to the **library** (building meetings' notes go to the building's filing cabinet) — again because buildingId is null, not because of the kind. | Same blocks, but the in-tray is the Town Hall's (managers' rollups and proposals) plus each building's pending count. Step 1 differs: **"open with 'Decisions needed from the humans'"**, yes/no questions from the Needs and in-tray, then a short agenda; "settle agent-to-agent back-and-forth outside the meeting". Facilitator: first active building manager among the invitees. | The "Decisions needed from the humans" opener is the only kind-specific behaviour. Caveat: Building → Meetings lets you pick `town-hall` inside a lab (you get a lab standup with the humans-decision opener) or `standup` in the Town Hall (a town hall without that opener). |
| **one-on-one** (1:1) | One human and the building's manager agent. Opened only by "Talk to ★" (`POST /api/buildings/:id/one-on-one`, needs `meeting.facilitate` or `building.review`, human only, the building must have a manager); never scheduled, not in the Call meeting dropdown (the API refuses it). | Nothing: no summaries; created straight into `discussing`. | Same `decide` (assignments, waitFor, supersedes). The manager **cannot `end`** it: the human ends it (or the town closes it when it goes quiet). Notes doc as usual. | No facilitation session. The manager's own manage session answers each human line (`oneOnOnePrompt`), resumes after a restart and lists unanswered lines. | Only the manager and that human may speak; manager doesn't go `in-meeting`; survives redeploys by resuming. |

Common to all non-1:1 kinds: invitees get an inbox message "Submit a short **standup** summary…", bodies walk to the meeting room, the facilitator (building manager, else reviewer, else first resident) runs a ≤60-turn session with town verbs only, `@Name` from the facilitator or a human gives that attendee a short read/search reply turn (≤5 per meeting), an agent facilitator may not end while a human spoke in the last 5 min or is typing, and the runtime closes the meeting with notes if the facilitator doesn't.

## Proposal: one "Call a meeting" form

One form, in both places that call meetings today (Building → Meetings and the empty meeting room). Fields:

1. **Preset** (optional, first): Standup, Town hall, Review the in-tray, Retro, Planning, Blank. Picking one pre-fills the fields below; every field stays editable. The preset is stored as `kind` (a label for history and filters), never as behaviour.
2. **Title** (pre-filled "<building> <preset>").
3. **Agenda**: a list of free items a human adds at start (add/remove rows). Shown to the facilitator in the opening prompt as numbered items it must cover in that order before proposing its own; shown in the meeting panel; written into the notes. Empty = today's "propose 2–4 items".
4. **Attendees**: the existing picker, pre-filled by the preset (building residents; Town Hall: managers + reviewers + moderators).
5. **What each attendee brings**: one choice plus an optional line of text: *Status update* (today's Did/Next/Need), *Nothing* (go straight to discussion, no 3-minute collecting), or *Custom* ("Bring: the one thing that went worst this week and why"). The text replaces the Did/Next/Need instructions in the summary prompt.
6. **Ask the humans for decisions** (checkbox): the "Decisions needed from the humans" opener, today hard-wired to kind town-hall.

Presets (what they pre-fill):

| Preset | Attendees | Brings | Agenda | Decisions opener |
|---|---|---|---|---|
| Standup | building residents | status update | — | off |
| Town hall | managers, reviewers, moderators | status update | — | on |
| Review the in-tray (Mitchell's ask in mt_6830h8x5qk) | Town Hall managers | nothing | "Read each in-tray item in one line with its ask; the human says approve / fund / counter / cut / later" | on |
| Retro | building residents | custom: "what went well, what went badly, one thing to change, with evidence" | — | off |
| Planning | building residents | custom: "the work you propose next and its cost in tokens" | — | on |
| Blank | picked by hand | nothing | — | off |

The 1:1 stays its own button ("Talk to ★"); it is not a preset because it is a different mechanism.

### Code changes for step 2

- **Schema** (`schema/src/index.ts`): `Meeting.agenda` stays a string (items as numbered lines, so old meetings and the notes format need nothing); add `Meeting.brings` (`{mode: "status"|"nothing"|"custom", text: string}`, default status) and `Meeting.askHumans` (boolean, default = kind is town-hall). `MeetingKind` adds `"in-tray-review"` and `"ad-hoc"` (labels). `CreateMeetingInput` takes `agenda` as string or string[], `brings`, `askHumans`. `MeetingCadence` unchanged.
- **Migration 044**: `ALTER TABLE meetings ADD COLUMN brings TEXT` and `askHumans INTEGER`; store.ts adds them to json/bool. Check `git ls-tree origin/main packages/core/migrations/` for the number first.
- **Core**: `createMeeting` stores the fields, defaults `askHumans` from kind; mode `nothing` creates straight into `discussing`; the invite message says what to bring instead of "standup summary". `prompts.ts`: `summarySystemPrompt` takes `brings` (status = today's text, custom = the human's line); `facilitatePrompt` branches on `askHumans`, not `kind === "town-hall"`, and renders agenda items as "Cover these, in order, before your own items". A `MEETING_PRESETS` table in core (shared with web) is the single source for the presets.
- **Runtime**: `onMeetingStart` skips summaries for `nothing`; `summarize` passes `brings`.
- **Web**: one `CallMeetingForm` component replacing MeetingsTab's dropdown and MeetingPanel's CallMeeting button: preset select, title, agenda rows, AttendeePicker, brings, opener checkbox. Meeting panel shows agenda items (already shows `agenda`) and "Attendees bring: …". Mock server and fixture.
- **Tests**: core createMeeting defaults per preset, facilitate prompt with agenda items and askHumans off/on, summary prompt with custom brings; runtime: `nothing` skips collecting.
- **Docs**: docs/meetings.md §7 "One form, presets".

**Estimate**: 1 session for core + schema + migration + prompts + tests, 1 session for the web form and mock; about 300–450k adjusted tokens total, plus a live-check session (a human calls an "Review the in-tray" meeting with two agenda items and sees them in the facilitator's first line and in the notes). Uncertainty: ±50%, mostly the web form.

