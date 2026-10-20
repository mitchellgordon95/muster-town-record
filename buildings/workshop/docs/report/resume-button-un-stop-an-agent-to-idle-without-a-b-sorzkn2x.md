---
id: "dc_s3sorzkn2x"
type: "report"
state: "building"
title: "Resume button: un-stop an agent to idle without a bogus task (PR #33)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:30:32.958Z"
sessionId: "se_78cca77zvu"
assignmentId: "as_37ava78i56"
costUsd: 0.44617929999999995
tokens: 788000
turns: 22
createdAt: "2026-10-20T04:24:21.774Z"
updatedAt: "2026-10-20T04:30:32.958Z"
---
## What I did
Checked the code: there was no way to un-stop an agent except giving it work (`POST /agents/:id/work` clears `stopped` as a side effect, and with no input it creates a "Check in" assignment) or replying to one of its reports. So I added a real resume and opened PR https://github.com/mitchellgordon95/agent-town/pull/33.

## Findings
**Before this PR:** you couldn't. Any route out of `stopped` created an assignment.

**PR #33 adds:**
- `POST /api/agents/:id/resume` (`ops.resumeAgent`): moves `stopped` to `idle` and creates no assignment. It needs the same permission as stop: `building.assign` or being the agent's owner. For any other status (`idle`, `banned`, `retired`, `out-of-budget`) it does nothing and returns the agent unchanged.
- **Resume button** on a stopped agent's Activity panel, shown when you have control. The mock API supports it too.
- **One thing to know:** a plain Stop doesn't cancel pending assignments. A "stop" decision from the in-tray does. So if the agent still had a `pending` assignment when you stopped it, the scheduler starts that within about 5 s of Resume. If you want it fully quiet, cancel those assignments first.

**Verified:** `npm run typecheck` is clean and all tests pass. I added new cases in `packages/core/test/reply.test.ts` (resume goes to idle, no assignment is created, banned stays banned, a non-controller is forbidden) and `packages/server/test/desk.test.ts` (stop then resume over REST gives idle with the same assignment count).

**I opened a PR rather than pushing to main.** The session's code-access rules say never push to main, and that clashed with the standing rule to push straight to main.

## What I need from you
Merge PR #33.

## Reply from Mitchell (2026-10-20 00:30)

merge

