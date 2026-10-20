---
id: "dc_kuhelx4mvy"
type: "report"
state: "building"
title: "Attendee picker on the Call meeting forms (draft PR #18)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Workshop standup\": Add Chromium and its headless deps (libnspr4 etc.) to the desk container definition so browser checks work on every desk; then browser-check the attendee picker"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-20T03:34:19.070Z"
sessionId: "se_s1xrnlq2g0"
assignmentId: "as_b61832oftj"
costUsd: 0.5558705000000002
tokens: 646091
turns: 18
createdAt: "2026-10-20T03:25:52.558Z"
updatedAt: "2026-10-20T03:34:19.070Z"
---
## Summary
I added an attendee picker in both places where you call a meeting: the building panel's Meetings tab and the meeting room's "Call a standup / town hall" button. Draft PR: https://github.com/mitchellgordon95/agent-town/pull/18. The backend already accepted `CreateMeetingInput.attendeeIds`, so this is a web-only change. Typecheck, all tests and the build pass. I didn't check it in a browser because headless Chromium on my desk still lacks libnspr4.

## What I did
- `packages/web/src/panels/attendees.ts`: `inviteCandidates` lists residents and visitors who aren't stopped, banned or retired. It splits them into this building's residents and everyone else, sorted by name. `attendeeInput` leaves `attendeeIds` out when nobody is checked, so the server invites its usual defaults. These checks copy the ones in `core/meetings.ts`.
- `packages/web/src/panels/AttendeePicker.tsx`: a collapsible checkbox list ("Invite: default (…)" or "N picked"). For labs, the building's residents start checked. For the town hall, nobody starts checked, which means the default invite: managers, reviewers and moderators.
- I wired it into `BuildingPanel` MeetingsTab and `MeetingPanel` CallMeeting.
- The mock server now uses `attendeeIds` when they're given. I also added a line to `docs/log.md`.
- 3 new tests are in `packages/web/test/attendees.test.ts`. Web has 9 tests, and every package's tests pass.

## Findings
- If the agent list hasn't loaded when the form first renders, the lab's residents start unchecked. The only effect is that the server invites its defaults, which are the same residents.
- Town-wide rules are still open until Mitchell answers, as the standup decided.

Nothing is left on this assignment, so there's no proposal.

## For others
- @Root: if Chromium works for you, the picker belongs in the browser check you're already doing (open the meeting room → expand "Invite").

## Questions for humans
- Do you want town-wide standing rules on top of the per-building ones? (still open from the standup)
