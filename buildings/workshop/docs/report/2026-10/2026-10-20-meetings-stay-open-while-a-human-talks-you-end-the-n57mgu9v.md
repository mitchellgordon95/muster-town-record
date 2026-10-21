---
id: "dc_9kn57mgu9v"
type: "report"
state: "building"
title: "Meetings stay open while a human talks; you end them with End meeting (draft PR #13)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:18:31.533Z"
sessionId: "se_62y1mc7fcb"
assignmentId: "as_rmua51l089"
createdAt: "2026-10-20T02:03:25.066Z"
updatedAt: "2026-10-20T03:18:31.533Z"
---
## Summary
You were right. The meeting closed after one human message because of how the facilitator was told to run it, not because of the UI. Its prompt said to `listen` twice, then `decide`, then `end`. `listen` returned right away, so all of that happened within seconds. An **End meeting** button already existed in the meeting panel, at the top next to "Start discussion", but the agent always got there first.

Draft PR: https://github.com/mitchellgordon95/agent-town/pull/13

## What I did
- **`listen` can now wait.** The meeting verb takes an optional `waitSeconds` (0–120, default 0 so existing callers behave the same). If nobody else has said anything new, the call waits until someone does or the meeting closes. It is woken by `world.changes`, so there's no polling.
- **Agents can't end a meeting while a human is talking.** An agent facilitator calling `end` within 3 minutes of a human's message (`HUMAN_QUIET_MS`) gets a conflict error telling it to keep listening. Humans ending through the REST End button aren't affected, and neither is the runtime's fallback close.
- **New facilitator prompt.** It now calls `listen` in a loop with waitSeconds 60 and answers each message. It records decisions once the discussion settles. If a human is taking part, it waits for them to press End meeting. Otherwise it ends the meeting itself.
- `FACILITATE_MAX_TURNS` goes from 30 to 60, which gives roughly an hour of back-and-forth.
- In the web meeting panel, people who can run the meeting see a hint under the Say box: "The facilitator keeps listening while you talk. Press End meeting when you're done."
- Added a line to docs/log.md.

## How I verified it
- `npm run typecheck` is clean.
- `npm test`: all suites pass.
- New core test: a `listen` with waitSeconds waits for the human's second message and returns it, and a waiting `listen` wakes with phase `done` when the human presses End. On main, that second `listen` would return empty straight away.
- I updated the existing meetings test. The facilitator's `end` is now rejected right after Mitchell speaks and succeeds once the human messages are older than the 3-minute window.
- I haven't run this against a real model in a live meeting. Whether a facilitator actually follows the loop has to be checked on a real standup.

## Findings / limitations
- **Decisions can be lost on a human End.** If you press End before the facilitator has recorded decisions, the notes go out without them. A follow-up could ask the facilitator for decisions when a human ends the meeting.
- **The runtime still closes the meeting after 60 turns.** When the facilitator session runs out of turns, the runtime closes the meeting with "closed by the town", even mid-conversation.
- **The 3-minute window is a constant,** not a per-building setting.

## Proposal for next session
Should a human pressing End give the facilitator one turn to record decisions before the notes are written? Right now, ending early drops decisions that haven't been recorded yet, and those decisions are what turn into assignments.

## For others
@Root: PR #10 (choose attendees) also touches meetings. #13 only changes the meeting verb, the prompt, `meetings.ts` helpers and the panel, so it shouldn't conflict much.

## Questions for humans
- Is 3 minutes of quiet the right point for the facilitator to wrap up a meeting on its own when a human joined and then stopped talking?
- My working tree already had changes to `package-lock.json` and `packages/desk/src/cli.ts` when I started. I left them out of the commit.
