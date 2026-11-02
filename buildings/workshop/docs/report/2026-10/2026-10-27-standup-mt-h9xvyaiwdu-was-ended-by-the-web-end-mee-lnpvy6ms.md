---
id: "dc_cllnpvy6ms"
type: "report"
state: "building"
title: "Standup mt_h9xvyaiwdu was ended by the web \"End meeting\" button, not a bug; endMeeting now records who ended a meeting (ceadf58 → main cf9267f)"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Finding accepted: a human End click, not a bug; cf9267f records who ended a meeting. Decision: keep the button, add a confirmation while a meeting is still collecting (assigned to Root). The proxy-chat test is already fixed on main by 9f72eaa."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T00:01:39.837Z"
sessionId: "se_jmup2s055v"
assignmentId: "as_xcec24rmo4"
costUsd: 1.0229787000000001
tokens: 62474
turns: 33
createdAt: "2026-10-27T00:00:04.962Z"
updatedAt: "2026-10-27T00:01:39.837Z"
---
## What I did
- Read the code paths that end a meeting and the live event log for 00:57Z (events 17268–17270).
- Changed the code so every meeting end records who ended it, added a test, and pushed straight to main: ceadf58, merged as **cf9267f**. A redeploy was already waiting, so I'm stopping here rather than waiting for it.

## Findings
**What ended mt_h9xvyaiwdu: a human pressed End, very likely Mitchell. It was not a bug.**
- At 00:57:11.713Z, us_1la74k332n (Mitchell) called the meeting (`meeting.created`, phase collecting). At 00:57:15.091Z the notes [dc_kv7sxrtacd](../../meeting-notes/2026-10/2026-10-26-town-workshop-standup-notes-7sxrtacd.md) were written, and at 00:57:15.092Z the meeting went collecting → done. `startedAt` is null, so it never reached the discussion. Nothing else happened in the log in between: no session, no tool call, no summary.
- I ruled out the other paths:
  - The runtime's own close (`facilitate`) only runs on discussing meetings, and it would have added the closing line "…closed by the town.".
  - The quiet-1:1 close is for 1:1s only, and it also adds a closing line.
  - The `meeting end` verb needs a running agent session, and there was none.
  - The drain only posts lines into meetings; it never ends them.
- What fits: the notes have no Closing section, which matches POST /api/meetings/:id/end with no body. That is what the web **End meeting** button sends (MeetingPanel.tsx:152). The button is shown even while the meeting is collecting, right next to the disabled Say box.
- The notes list Pix as author because `ops.endMeeting` passed a null actor, so the notes fell back to the facilitator. The live log cannot prove the click was Mitchell's: before this change it recorded no actor. Mitchell called the meeting 3.4 s earlier, so it was most likely him.

**The change (ceadf58):**
- Each `meeting.phase` event now carries `payload.by` = {kind: user|agent|system, id}. If an agent ended the meeting, the event's `agentId` is set too, and the text ends "(by Mitchell)", "(by Pix)" or "(by the town: facilitation-end)".
- Where each path gets its `by` from:
  - REST and `ops.endMeeting`: the caller's holder (a human user id or an agent id).
  - The `meeting end` verb: the agent.
  - The runtime's own closes are named causes: `facilitation-end` and `quiet-1:1`.
  - Any other null-actor end is recorded as `town`.
- Tests:
  - New core test covering a human ending a meeting while it's collecting, the facilitator ending it via the verb, and a named town cause. Core meetings tests pass 14/14.
  - Typecheck passes for cli, core, desk, runtime and server. The full `npm run typecheck` hit my 400 s limit, so I ran tsc per package.
  - Runtime one-on-one tests pass. One runtime test fails: meetings-chat-scheduler "proxy chat … first person" expects 40 tokens and gets 960. It fails the same way on main without my change.
  - I did not re-run tests after merging main (23 files came in).
- No PR: the Workshop rule is to push straight to main.

## What I need from you
Decide whether "End meeting" should be hidden or ask for confirmation while a meeting is still collecting, since that's where this one-click close happened. (Also: the proxy-chat token test above is red on main.)
