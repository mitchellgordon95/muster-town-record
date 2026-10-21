---
id: "dc_2w2xo9uh1i"
type: "report"
state: "building"
title: "Meetings: call any time (already worked) + choose attendees (PR #10)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "the backend works but i don't think the UI supports doing another meeting after the first.\n\nalso let's get rid of agent titles, they don't need personalities really or job descriptions. in fact it's harmful, because of situations like this where an agent thinks they're only responsible for the backend but they're really responsible end to end\n\nalso is there some prompting compulsion to always invent something to do next? i don't think i like this setup"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T02:03:22.096Z"
sessionId: "se_d4avqdcb4l"
assignmentId: "as_raqhz84c2u"
createdAt: "2026-10-20T01:59:01.659Z"
updatedAt: "2026-10-20T02:03:22.096Z"
---
## Summary
Mitchell asked: "are we only set up for one standup a day? I want to call meetings whenever and choose who attends."
- **Calling meetings whenever: this already worked.** `POST /api/meetings` and the "Call meeting" button (building panel → Meetings tab, or the empty meeting room) start a meeting right away. Recurring meetings are set per building in `meetings: [{kind, everyMinutes}]`. `everyMinutes: 0` means manual only, which is the default for imported buildings. Nothing limits a building to one standup a day.
- **Choosing attendees: this was missing.** Every meeting invited all residents (for town hall: every manager, reviewer and moderator). **Draft PR #10 fixes the backend:** https://github.com/mitchellgordon95/agent-town/pull/10

## What I did
- `packages/schema`: `CreateMeetingInput.attendeeIds?: Id[]` (at least 1).
- `packages/core/src/meetings.ts`: when `attendeeIds` is given, duplicates are removed and every id is checked. It must be an existing resident or visitor agent that is not stopped, banned or retired. Unknown ids get a 404; anything else invalid gets a 400. No meeting or invites are created on error. If the list is omitted, the old defaults apply. The facilitator is still the building's reviewer even when they aren't on the list (the runtime already adds the facilitator on top of the attendees).
- Tests: 2 new core tests (only the chosen agents are invited, others aren't, duplicates removed, defaults unchanged, the empty/unknown/human/stopped rejections, nothing written on error) and 1 REST test (201 / 404 / 400).
- Updated docs/architecture.md and added a line to docs/log.md.
- Verified: `npm run typecheck` is clean and `npx vitest run` passes (23 files, 128 tests).

## Findings
- Humans are rejected as invitees on purpose. The runtime starts a cheap-model summary session for every attendee, so a human avatar on the list would get a model-written summary. Humans join a meeting through `say`.
- The web UI has no attendee picker yet. Until it does, choosing attendees only works through the API.

## Proposal for next session
**Renumber migration `004_doc_turns.sql` to `007` in PR #2 so that live DBs (already at version 6) actually get `docs.turns`.** Pix flagged this: `migrate()` skips files numbered at or below the DB's current version. It's a real lost-update bug on live DBs. Add a test that migrates a DB already at v6.

## For others
- @Pix: please add an attendee multi-select to the "Call meeting" form in BuildingPanel `MeetingsTab` and MeetingPanel, wired to `attendeeIds` (I sent you a tell).
- @Sage: architecture.md is updated in PR #10 for the new field.

## Questions for humans
- Should agents in other buildings be invitable to a building's meeting? The PR currently allows it (any active resident or visitor). Say if you'd rather limit it to that building's residents.
- Do you want a recurring cadence on the Workshop (e.g. a standup every 24 h), or are manual meetings enough?
