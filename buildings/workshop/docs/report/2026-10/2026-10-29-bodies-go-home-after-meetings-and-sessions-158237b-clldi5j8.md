---
id: "dc_xmclldi5j8"
type: "report"
state: "building"
title: "Bodies go home after meetings and sessions (158237b, PR #90); live check parked"
authorId: "ag_2qifxtr4vw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #90 / 158237b merged for Mitchell's flag dc_ihwq7bfi4o; the live check is already parked as as_lnwhlvbw89 (waits deploy 158237b), so no new assignment. Rollup 31 Shipped candidate once the live check and screenshot land."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T21:28:56.772Z"
sessionId: "se_i73vnjtgju"
assignmentId: "as_rx4w0sc7sw"
costUsd: 2.742796400000001
tokens: 137140
turns: 69
createdAt: "2026-10-29T21:28:31.866Z"
updatedAt: "2026-10-29T21:28:56.772Z"
---
## What I did
I checked the live town against Mitchell's flag [dc_ihwq7bfi4o](../../flag/2026-10/2026-10-29-for-some-reason-i-see-a-bunch-of-managers-lingerin-wq7bfi4o.md) and found the code paths behind it. I added a "walk home" rule in core, with tests, and merged PR #90 (https://github.com/mitchellgordon95/muster-town/pull/90) as 158237b after CI passed (run 40957692343, 2m14s). A plain redeploy is queued. The live check is parked until 158237b is deployed.

## Findings
- **Live at 20:30Z (GET /api/town):** five managers were idle around (55–61, 32–34), at the Town Hall meeting room (59,34): Pix, Kelly, Cleo, Nell and Mara (Mara's last activity was "In the meeting", 20:12Z). Town hall mt_e1uoil9mx5 had ended about 20:19Z. The forks were all at their own desks.
- **Why they stayed:** nothing walks a body home.
  - When a meeting ends, core `setMeetingPhase` (done) only sets the status back to idle.
  - The cleanup in runtime `facilitate` (runtime/src/meetings.ts) only cancels walks still in progress.
  - The only walk to a desk is runtime `walkToDesk`, and it runs only when a work session starts.
  - Manage sessions and `endSession` never move the body. So a manager stays wherever the last meeting or `go` left it. Retired forks free their desk and leave the map, so they don't add to this.
- **The fix, in a new file core/src/home.ts:**
  - `walkHome` runs when a meeting ends (done or cancelled), for attendees and the facilitator. It also runs when any session ends (`ops.endSession`) and after facilitate's cancel loop.
  - `walkIdleHome` runs on every runtime tick (5 s) and sends home idle residents who are away from their desk.
  - A body stays where it is if it is in a meeting, walking, in a running session, has no desk (visitors, humans, Ada), or talked in the last 2 min (a `say`, or a `go` to another agent).
  - To detect the `go`, `agent.moved` events now carry `toAgentId`.
  - No schema change, no Bank change, and no other building's code.
- **Tests:**
  - The new core test/walk-home.test.ts has 4 tests and passes.
  - Rerun with a longer timeout, the core meetings, one-on-one, verbs, forks and presentation suites pass (69/69), and so does all of runtime (150/150).
  - The full `npm run check` on this 2-CPU desk had 58 failures, all at the 5 s test timeout and none an assertion. CI ran the full suite and passed.
- **Next session:**
  - Confirm GET /api/health shows 158237b or later.
  - Confirm GET /api/town shows no idle resident standing within 3 tiles of (59,34).
  - Take one cropped map screenshot (≤300 px tall) for rollup 31.
- The topic page [dc_8qwqtmh7i5](../../wiki/2026-10/2026-10-28-meetings-writing-indicator-who-ended-it-restart-dr-wqtmh7i5.md) is rewritten with the diagnosis and the rule.

## What I need from you
Nothing needed.
