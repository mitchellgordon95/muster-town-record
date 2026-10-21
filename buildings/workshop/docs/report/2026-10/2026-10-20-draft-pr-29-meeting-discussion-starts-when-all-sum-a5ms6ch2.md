---
id: "dc_8ka5ms6ch2"
type: "report"
state: "building"
title: "Draft PR #29: meeting discussion starts when all summaries are in; no chat while collecting; plain standup summaries"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:18:19.297Z"
sessionId: "se_t42xfaloyv"
assignmentId: "as_ix4ujvmzl1"
costUsd: 0.8409338000000001
tokens: 1593851
turns: 30
createdAt: "2026-10-20T04:15:54.024Z"
updatedAt: "2026-10-20T04:18:19.297Z"
---
## What I did
I made the three meeting-flow changes decided at the Town Workshop standup and opened draft PR #29: https://github.com/mitchellgordon95/agent-town/pull/29

## Findings
- **The discussion starts as soon as all summaries are in.** When the last attendee submits a summary, the meeting moves from collecting to discussing straight away, and the facilitator session starts from that event. The 3-minute wait is still there as a fallback, for when a summary call fails or an agent is out of budget. Code: `packages/core/src/verbs/meeting.ts`.
- **No chat until the discussion starts.** While a meeting is collecting, anyone who tries to speak gets a 409 error saying "still collecting summaries". This applies to humans and agents alike. In the web meeting panel, the say box and button are greyed out with the placeholder "Chat opens when the discussion starts…". The End meeting button still works. Code: `packages/core/src/meetings.ts` and `MeetingPanel.tsx`.
- **Shorter summaries.** The new summary prompt asks for two short lines in plain language: "Did: …" and "Next: …". A third line, "Need: …", is added only if the agent is blocked or a human has to act. Each line stays under 20 words, with no ids, file paths, jargon or long numbers. The invite message, the tool description, README, `docs/architecture.md`, `docs/design.md` and `docs/log.md` all match the new flow.
- **Tests:** `npm run typecheck` is clean and `npm test` passes in every package (core 81, runtime 30, server 26, web 20, cli 9).
  - A new core test checks that nobody can speak while collecting and that the last summary moves the meeting to discussing.
  - Two existing tests changed because they relied on the old behaviour. The runtime flow test now expects discussing right after the summaries. The REST test now checks that speaking while collecting gets a 409, then starts the meeting and speaks.
  - In the cadence test, the dummy summary text is now empty, so the meeting stays in collecting and the test still checks that no second meeting is created.
- **Behaviour change:** humans used to be able to speak while summaries were being collected. Now they have to wait for the discussion, as decided.
- **Not checked in a browser:** the web dev mock server still accepts speech while collecting. The real UI blocks it, so I left the mock as is.

## What I need from you
Review and merge PR #29.

## Reply from Mitchell (2026-10-20 00:18)

merge

