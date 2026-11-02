---
id: "dc_nl7u504rah"
type: "report"
state: "building"
title: "Meeting closed under Mitchell: facilitator end ignored unsent drafts; fixed on main 660913b (redeploy queued)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:02:10.757Z"
sessionId: "se_8m4kuzy2bj"
assignmentId: "as_z202iiae7o"
costUsd: 0.7618153999999999
tokens: 45125
turns: 27
createdAt: "2026-10-21T04:00:04.387Z"
updatedAt: "2026-10-21T04:02:10.757Z"
---
## What I did
I rebuilt the timeline of mt_mkvhpled0l from the server event log and read the meeting end path (core meetings.ts, verbs/meeting.ts, the facilitator prompt, and the web MeetingPanel). Then I fixed it and pushed **660913b** straight to main. I also called redeploy. 660913b should be live once the drain finishes, but I haven't checked that yet.

## Findings
**Root cause:** Pix, the agent facilitator, called `end`. Nothing was auto-ending the meeting.
- 03:51:52Z: the discussion opened.
- 03:51:55Z: Pix posted the agenda.
- 03:51:56Z and 03:52:57Z: Pix ran two 60 s `listen` calls.
- 03:54:00Z: Pix noted "Quiet; no humans speaking", recorded decisions, and called `end` at 03:54:03Z.
- 03:54:48Z: Mitchell's message landed, in the next meeting.

The only thing guarding `end` is `humanStillTalking`, which checks whether a human message was *sent* in the last 5 minutes. Mitchell hadn't sent anything yet, so the guard passed. The server had no way to know about typing or an unsent draft. The prompt's "once humans have been quiet for a few minutes" rule also counts nothing before a human's first message.

Humans could already close meetings: the End meeting button is there for facilitators and building managers. That part needed no change.

**The fix (660913b):**
- New route `POST /api/meetings/:id/typing` (returns 204). Only human callers count.
- The web say box pings that route every 10 s while it holds a non-empty draft.
- An agent's `end` is refused (conflict, "A human is typing…") while the last ping is under 30 s old. This is on top of the existing 5-minute hold after a human speaks.
- `listen` and `status` now return `humanTyping`, and the facilitator prompt tells the agent to keep listening while it's true.
- Typing state is kept in memory, so a restart can only shorten a hold.
- I added a core test covering: block while typing, an agent can't fake the signal, and the hold lapsing.
- Typecheck is clean, and the core and server tests pass: 284/284.
- docs/architecture.md and docs/log.md are updated.

**Gap:** this only covers people typing in the web panel. A human who is in the meeting room but idle, with an empty box, can still be closed on after they've been quiet.

## What I need from you
Nothing needed.
