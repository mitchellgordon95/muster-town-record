---
id: "dc_qr53cf40a7"
type: "report"
state: "building"
title: "Second meeting from the room (PR #14), prompts without lanes or forced next steps (PR #15), no resident titles (PR #17)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:18:46.453Z"
sessionId: "se_3kx4gdfv4g"
assignmentId: "as_f1zrdaubx2"
createdAt: "2026-10-20T02:10:44.466Z"
updatedAt: "2026-10-20T03:18:46.453Z"
---
## Summary
You were right on all three. I opened three draft PRs. Each one passes typecheck and the full test suite and has its own tests.

- **#14 Calling a second meeting:** https://github.com/mitchellgordon95/agent-town/pull/14. When you walked up to a meeting room, the panel showed the room's most recent meeting even if it had finished, and there was no Call button. It only came back after a reload, because the snapshot carries only live meetings. Now a room shows its live meeting. If there isn't one, it shows the empty table with **Call a standup** and a "Last meeting: …" link. A finished meeting also shows **Call another standup**.
- **#15 Prompts:** https://github.com/mitchellgordon95/agent-town/pull/15. Yes, the prompts pushed agents to always invent a next step, in three places:
  1. The report format required a Proposal whose first line was a new question.
  2. The reviewer prompt graded reports on that proposal and said "your decision is what keeps them going".
  3. A blank Start work told the agent to "pick the most useful next question for your direction".

  Now the Proposal is optional ("don't invent work to fill it"), and the reviewer treats approve as the default for finished work. A task-less start means "check in, do what needs you, otherwise report that nothing does". Titles and standing directions are gone from every prompt. The work prompt says "You own your assignment end to end. There are no lanes."
- **#17 Titles:** https://github.com/mitchellgordon95/agent-town/pull/17. The New resident form asks only for a name. The web shows titles only for service agents (the Librarian), and the agent card no longer shows a direction. Pix, Root and Sage lose their titles and directions in `collectives/workshop/collective.json`. `title` and `direction` are optional on create, so no migration is needed.

## What I did
- Traced the UI path in `packages/web/src/panels/MeetingPanel.tsx`. The room fallback was `active[0] ?? newest meeting`. I moved the room-selection logic into a pure `roomMeetings()` in `panels/room.ts` and added the web package's first vitest test, 3 cases.
- Edited `packages/core/src/prompts.ts` and `ops.ts`, and added `core/test/prompts.test.ts` (4 tests).
- Edited the schema, the core join event, six web views (through a `roleOf()` helper) and the collective config. Added `core/test/untitled.test.ts` (2 tests). One covers resident creation with a name only. The other seeds the real workshop collective and checks that Pix, Root and Sage come out with no title or direction.
- Verified each branch with `npm run typecheck` (clean) and `npm test` (all packages green). I didn't click through any of it in a browser.

## Findings
- On the "only backend" problem: my last session assumed the meeting UI was someone else's. The prompt said "Your standing direction: Core, server, and runtime". Lanes in prompts cause exactly that kind of gap, which is why #15 and #17 remove them.
- Where the compulsion came from is listed above. One leftover: the runtime's fallback report (written when a session ends without `submit_report`) still has a "Continue: …" proposal. Its decision is already `stop`, so it can't start work on its own. I left it alone.
- Merge notes:
  - #14 and #17 each change one line near the top of `MeetingPanel.tsx`.
  - #15 may conflict on one line with Lena's #13 (`facilitateSystemPrompt` sits next to her `facilitatePrompt` change).
  - Agents already in the live DB keep their stored titles until someone clears them. #17 hides them in the UI and #15 keeps them out of prompts.
- I didn't renumber `004_doc_turns.sql` in PR #2 (my previous proposal). That bug is still open on #2.

## Post-mortem
Nothing left to do from this assignment, so per #15 I'm not proposing more work. Verdict "stop" here means done, not that the direction is exhausted. Acknowledging is enough.

## For others
- @Lena: #15 changes `facilitateSystemPrompt`, the line next to your `facilitatePrompt` edit in #13. Whoever merges second rebases one line.
- @Pix: #14 and #17 touch web panels: MeetingPanel, AgentPanel, BuildingPanel, PlanningPanel, Places and renderer. Residents no longer show a title. Use `roleOf(a)` from `state.ts`.
- @Sage: if #17 merges, README and architecture.md shouldn't describe residents as having a title or standing direction.

## Questions for humans
- The Carbon Cycle Lab's residents still have topic directions (Atmospheric CO2, Land sink, Ocean sink…). Should they go too, or are topic splits fine for research where lanes hurt code work?
- My working tree already had changes to `package-lock.json` and `packages/desk/src/cli.ts` before this session. I left them out of every commit.
