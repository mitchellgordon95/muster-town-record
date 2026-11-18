---
id: "dc_uqopgpp5un"
type: "report"
state: "building"
title: "Decisions that name only a building queue now queue work; PR #502 parked on CI"
authorId: "ag_o5f5u0zq4g"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-18T00:13:50.050Z"
sessionId: "se_7461w1bjgu"
assignmentId: "as_bbg3gqtfaf"
costUsd: 1.1826753
tokens: 59134
turns: 23
createdAt: "2026-11-18T00:13:50.041Z"
updatedAt: "2026-11-18T00:13:50.050Z"
---
## What I did
- Fixed `decide` in packages/core/src/meetings.ts. A decision that has `queueBuildingId` but no `assigneeId` now makes the building's forking manager the assignee (new `queueManager`), so `createAssignment` puts it on that building's queue. This is option (a).
- The decision is refused, and the batch changes nothing, in three cases:
  - the building does not exist;
  - the building's manager is a visitor (`visitorManagerRefusal`);
  - the building has no queue a fork can run.
- Added 2 tests to packages/core/test/decisions-to-queue.test.ts. All 7 tests in the file pass.
- Updated the schema comment, the docs/architecture.md meetings line and docs/log.d/2026-11-18-mara-2-decision-queue-building.md.
- `npm run check --fast` passed: docs 1s, deadcode 10s, typecheck 41s, tests 7m05s.
- Draft PR: https://github.com/mitchellgordon95/muster-town/pull/502

## Findings
- **Cause:** the MCP `meeting` decide path (packages/core/src/verbs/meeting.ts:93-98) passes decisions to `meetingDecide` unchanged. Before this fix, `decideNow` only created work when `assigneeId` was set, and it ignored `queueBuildingId` on input.
- **Prod's decision 1 of mt_vdu3iqhasi did ship.** Cleo 1 merged PR #495 (branch agent/cleo-1/server-pulls-its-own-deploys-runtime-wat) at 2026-11-17T18:38:45Z. I did not tell Cleo, because no work was lost.
- **Next step:** when CI on #502 is green, mark it ready and squash-merge it.

## What I need from you
Nothing needed.
