---
id: "dc_ejztdkgrnx"
type: "report"
state: "building"
title: "Facilitator can question attendees with @Name mid-meeting (PR #22)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:50:32.204Z"
sessionId: "se_deqbktqlcx"
assignmentId: "as_1rsxanvg7t"
costUsd: 0.8223691000000001
tokens: 1250773
turns: 26
createdAt: "2026-10-20T03:45:39.734Z"
updatedAt: "2026-10-20T03:50:32.204Z"
---
## What I did
Built the feature in the runtime and core prompts, added 2 tests, updated architecture.md and log.md, and opened draft PR https://github.com/mitchellgordon95/agent-town/pull/22. It doesn't touch any of the web files in #21.

## Findings
- **How it works:** the facilitator or a human writes `@Name` for an attendee while a meeting is collecting or discussing. That attendee then gets one `meeting-reply` session, and its answer is posted into the meeting transcript. The facilitator picks it up on its next `listen`.
- **What the reply sees:** the last 20 utterances, the agent's current assignment, its latest report and its last 20 events. It runs on the agent's own model with no tools and a single turn (the same `oneShot` path summaries use). The cost goes on the agent's budget, and the reply is skipped if the agent's budget doesn't allow a new session.
- **Guards:**
  - Only mentions from the facilitator or a human wake an attendee. Attendees mentioning each other wakes no one, so replies can't set off chains.
  - The facilitator never gets a reply turn, and stopped, banned or retired agents are skipped.
  - A mention that arrives while a reply is still running gets one more turn afterwards.
  - Each attendee gets at most 5 replies per meeting, and each reply is capped at 1200 characters.
- **Other changes:** the facilitator's prompt (step 2) now says it can question attendees this way. Sessions have a new purpose value, `meeting-reply`; the database doesn't constrain that field, so no migration is needed.
- **Checks:** `npm run typecheck` is clean and `npm test` passes in every package. The new tests cover:
  - a facilitator mention leads to a reply in the transcript, the prompt carries the context, and the reply had no tools;
  - an attendee's mention wakes no one;
  - a human's mention wakes the attendee, and the 5-reply cap holds.
- **Not checked:** I haven't run it with a real model in a live meeting.

## What I need from you
Review and merge PR #22.

## Reply from Mitchell (2026-10-19 23:50)

merge

