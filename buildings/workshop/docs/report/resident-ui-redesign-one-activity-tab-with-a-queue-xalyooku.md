---
id: "dc_ggxalyooku"
type: "report"
state: "building"
title: "Resident UI redesign: one Activity tab with a queue/interrupt composer, Reports tab gone (PR #28)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:17:59.598Z"
sessionId: "se_g30r3e2evp"
assignmentId: "as_bpl4ph42r4"
costUsd: 2.0046711
tokens: 4182192
turns: 59
createdAt: "2026-10-20T04:13:51.208Z"
updatedAt: "2026-10-20T04:17:59.598Z"
---
## What I did
I built the resident UI redesign from the standup and opened draft PR #28: https://github.com/mitchellgordon95/agent-town/pull/28. Before committing I ran typecheck, the full test suite, and a check in a real browser against the mock server.

## Findings
- **Agent panel now has two tabs: Activity and Assignments.** The Reports tab is gone. Reports can still be found in the in-tray, in the filing cabinet, or in the library by author. The Dismiss button moved to the Assignments tab.
- **Activity, Chat and Session are now one timeline.** It shows the agent's events, the running (or last) session's transcript, messages you sent, and the desk assistant's replies. A composer sits at the bottom and works like Claude Code:
  - **While the agent works:** Enter queues your message, and the agent gets it when its current turn ends. **Interrupt & send** stops the current turn so the message runs right away. **Stop** is also there.
  - **While the agent is idle:** Enter asks the desk assistant. **Leave for next session** saves the message for the agent's next work session.
- **"Send now" works end to end, not just in the UI:**
  - The interrupt API takes a new `now` field, and the interrupts table gets a matching column (migration 009). I skipped 007 because no branch has it, and 009 can't collide with anything.
  - The desk's control response passes `now` along. Both host and desk sessions add the message to the queue first, then cut the current turn short. The Agent SDK's own documentation says queued messages survive an interrupt and still run.
- **Bug fixed along the way:** a session's error was only cleared when the session went on to another turn. So any session whose last turn followed a failed or interrupted turn ended as "error", even after it recovered. Now any successful turn clears the earlier error, in both host and desk sessions.
- **Verification:**
  - `npm run typecheck`: 0 errors.
  - `npm test`: 167 tests passed (80 + 21 + 31 + 26 + 9), 0 failed.
  - New tests: the desk and the host runtime each have one for send-now (the turn is cut short, the message runs next, and the session ends as done with no error). The server test now checks that the control response includes `now`.
  - In the browser (mock server): a working resident showed one queued message and one sent-now message in the timeline, and an idle resident's Ask got a reply.
- **Limits:**
  - A queued message keeps its "queued for the next turn" label after delivery. The UI gets no event when the agent actually takes the message in.
  - I only tested send-now with fake SDKs, never against the real CLI.
- **Not started:** token usage and budget stats on building cards and under resident names. That was a separate decision from the same meeting.

## What I need from you
Review and merge PR #28.

## Reply from Mitchell (2026-10-20 00:17)

merge

