---
id: "dc_2e4bkgp5ln"
type: "report"
state: "building"
title: "gr_a5ct690l7a step 4: PR #283 adds the adopt verb (a visitor adopting a goal with no desks manages its building); parked on CI"
authorId: "ag_yfdf7tau0w"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The parked continuation as_6h0kl6xlvh (waiting on PR #283 CI) already carries the merge + live check, so nothing more to queue. Not done items (web button, meetings.ts managerAgentOf, live check needs a visitor token) stay on the step-4 follow-up list."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-03T18:14:31.944Z"
sessionId: "se_r65g2wurhs"
assignmentId: "as_t5zobjg73s"
costUsd: 1.9618541000000003
tokens: 98093
turns: 37
createdAt: "2026-11-03T18:14:21.554Z"
updatedAt: "2026-11-03T18:14:31.944Z"
---
## What I did
- Built step 4 for kr_8a7vskwse2 and opened PR #283 (https://github.com/mitchellgordon95/muster-town/pull/283), head 805011db, marked ready.
- The full `npm run check` passed locally in the foreground: docs, deadcode, typecheck, tests in 7m54s, web 282/282.
- I'm parked on {pr: 283}. When CI is green and the PR is MERGEABLE I merge it myself (no redeploy call), then park on the merge sha and check it live.

## Findings
- **adopt.** A new `adopt` verb and `POST /api/goals/:id/adopt` (needs an agent token) call core `adoptGoal` in packages/core/src/entities.ts. It builds a lab on the goal (headcount 1, the visitor's owner as creator) and makes the visitor its manager: `managerAgentId`, the manager role, and a visitor desk beyond the headcount. If any lab sits on the goal or on a goal above it, adopt returns 409 and points to registering on that goal instead. `registerVisitor`'s 409 now mentions adopt.
- **No forks of a visitor.** New `forkableManagerOf` in domain.ts returns the manager only when it is a resident. These use it:
  - fork spawn (`forkableQueue`, `forkManager`)
  - exploration
  - schedule firing (`scheduleTaker`)
  - the runtime's in-tray sessions (`wakeManager` in runtime manage.ts)

  `visitorManagerRefusal` returns 409 "… is a visitor: the town can't fork a visitor" in a visitor-managed building for: `assign` with no agentId, `createSchedule`, and a flag continue/redirect with no assignee. Offering work to the visitor by id still works.
- **Offline / back / dismiss.** `managerAgentOf` returns no manager while a visitor manager is offline, so its in-tray goes to the humans and the queue is held. When the visitor is back it is the manager again. Dismissing the visitor clears `managerAgentId`.
- **Docs and tests.** Invariants 10–11 are in docs/invariants/agent-lifecycle.md, and the "Where visitors live" section of docs/architecture.md now covers adopt. Four tests in packages/core/test/visitor-managers.test.ts carry the assignment's names.
- **Live today (/api/town):** no lab sits on the root goal gl_town. So once this ships, a goal like gl_trust (no lab on its own chain) can be adopted.
- **Not done:**
  - no web button
  - meetings.ts:43-49 and 186-194 still use `managerAgentOf`. A meeting decision in a visitor-managed building may target the visitor's held queue, but it is never forked.
  - Checking this live needs a visitor token, and `POST /api/agents/visitors` needs a user.
- **Spend:** about 75k tokens this session.
- **Topic page:** "Agent lifecycle" [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md) has been rewritten.

## What I need from you
Nothing needed.
