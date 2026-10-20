---
id: "dc_rmhhgbqcxt"
type: "report"
state: "building"
title: "ssh-origin seed test (PR #4) + state-machine audit: 3 illegal-transition gaps fixed (PRs #6, #7, #9)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:17:41.691Z"
sessionId: "se_6clsip2slq"
assignmentId: "as_z4icoc6x22"
createdAt: "2026-10-20T01:53:45.250Z"
updatedAt: "2026-10-20T03:17:41.691Z"
---
## Summary
I opened four draft PRs. Each one is a single gap with a test, and each test fails on main and passes on its branch.
- **#4** https://github.com/mitchellgordon95/agent-town/pull/4: a seed test that forces an ssh origin (`git@github.com:me/agent-town.git`). It checks that seed stores the origin raw and that `composeWorkBrief` hands desks the https URL. Before this, the seed tests read this repo's own origin, which is already https on desks, so the conversion was never covered end to end. As a mutation check I removed `httpsRepoUrl` from `deskWorkspace`, and the new test failed.
- **#6** https://github.com/mitchellgordon95/agent-town/pull/6: `endMeeting` on a **cancelled** meeting wrote a meeting-notes doc and set `notesDocId`, and only then threw `conflict`. That left an orphan notes doc on the board. It now rejects before writing anything.
- **#7** https://github.com/mitchellgordon95/agent-town/pull/7: `meetingDecide` had no phase check. `decide` on a done or cancelled meeting still created assignments and auto-superseded the assignee's pending reports, and none of it showed up in the notes. It now returns `conflict`.
- **#9** https://github.com/mitchellgordon95/agent-town/pull/9: when an assignment was cancelled mid-session (stop or dismiss), `submit_report` flipped it from **cancelled to done** through the session's `assignmentId` fallback. Now only pending or active assignments become done. `setAssignmentStatus` also rejects any move out of done or cancelled.

## What I did
- I read `prompts.ts` (`httpsRepoUrl`, `deskWorkspace`), `seed.ts`, `meetings.ts`, `verbs/meeting.ts`, `domain.ts` and `verbs/social.ts`, and traced every caller of `setAssignmentStatus` (ops, docs, runtime/work.ts).
- I confirmed each gap with a throwaway repro test before fixing it. Each PR branches off `origin/main` on its own (`agent/root/meeting-end-cancelled`, `agent/root/meeting-decide-after-end`, `agent/root/assignment-terminal-guard`), and #4 is on my assignment branch.
- On every branch, `npm run typecheck` and `npm test` passed for all packages (core 57, plus the other three suites at 20, 26 and 23).
- package-lock.json and the cli.ts mode change are still uncommitted in my checkout and are **not** in any PR, as instructed.

## Findings
- What the code does now: illegal-transition rejection is uneven. `summary` and `speak` already reject ended meetings, and `accept_assignment` rejects terminal assignments. `decide`, `end`-on-cancelled and `setAssignmentStatus` had no guard until these PRs.
- Two remaining gaps I chose **not** to fix this session:
  1. `setMeetingPhase` allows backward moves (discussing → collecting or scheduled). It's only reachable through ops and the runtime, which only move forward.
  2. `startSession` with a done or cancelled `assignmentId` sets `currentAssignmentId` to it. After #9 it can't reactivate the assignment, but the agent's `look` would show a dead assignment.
- What I don't know: whether any human workflow relies on adding decisions to a meeting after it ends. If one does, #7 blocks it.

## Proposal for next session
Should `setMeetingPhase` enforce a forward-only phase order (scheduled → collecting → discussing → done, with cancelled reachable from any live phase), and should `startSession` reject a terminal `assignmentId`?
- Why it matters: those are the last two transitions in the audit that aren't guarded.
- Where to look: `packages/core/src/meetings.ts`, `ops.ts startSession`, and `runtime/src/meetings.ts` (to check that the runtime only moves forward).
- What would change the picture: finding a legitimate backward move, such as rescheduling a meeting.

## For others
- @Pix: #9 changes `setAssignmentStatus` so it throws on terminal → other status moves. If web or server code reopens assignments, it will now get a 409.
- The PRs are independent and touch different hunks, though #6 and #7 both edit `meetings.ts` and `meetings.test.ts`. If they merge in sequence, the second may need a trivial rebase.

## Questions for humans
- Mitchell: are the package-lock.json and `packages/desk/src/cli.ts` mode changes wanted? They're still sitting uncommitted in my checkout.
- Is adding decisions to a meeting after it has ended something you ever want? (That's #7.)
