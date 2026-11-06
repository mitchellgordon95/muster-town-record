---
id: "dc_jd5r85btnp"
type: "report"
state: "building"
title: "Decisions naming a forking manager go to its building queue: PR #369 open, parked on CI"
authorId: "ag_8cf0juzhih"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T20:49:05.941Z"
sessionId: "se_cu27xi66wo"
assignmentId: "as_9512zq0uf8"
costUsd: 1.8775582999999996
tokens: 93878
turns: 8
createdAt: "2026-11-05T20:30:15.703Z"
updatedAt: "2026-11-05T20:49:05.941Z"
---
## What I did
Built the fix from Mitchell's 1:1 mt_peubjyoo0k and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/369 (branch agent/pix-2/decisions-and-reviews-that-name-a-forkin). Told Mara (ms_2wcqy2jhrc) the two lines below for her work-routing map, as Pix asked. The PR is parked on CI.

## Findings
- **What it fixes:** two paths now put work on the building queue (a fork runs it) when it names a manager whose building forks:
  - meeting decisions (meetings.ts decideNow)
  - `review` continue/redirect on that manager's own report (domain.ts applyDecision)
  
  How it works: a new `decisionQueue(world, agentId)` in domain.ts. The decision keeps `queueBuildingId` (no migration, because decisions are stored as JSON). The notes, MeetingPanel, `meeting` status/decide output and the facilitator's "last meeting" prompt read "→ <building> queue (a fork of <manager>)". The `review` output also returns `queue`/`to`.
  
  Two side effects:
  - Such a decision no longer auto-approves the manager's own pending reports.
  - Amending a decision that a fork is already running now amends it instead of refusing with "already working".
- **What it leaves alone:** `createAssignment` still defaults to the agent's own queue. I did it per path instead because a default with a list of exceptions would silently move any future town job. Untouched paths that still default a manager's work to the manager:
  - tells/relays and @mentions (wakes.ts)
  - parked continuations of the manager's own work (submit_report resumeWhen)
  - `ops.createWork` (the human "give work" API)
  - the amended-decision wake (wakes.ts:229)
  
  The town's own manager jobs also stay on the manager by design: checkpoint, grant funded/countered/rejected, explore and schedules. The tells and the other paths above are the holes for Mara's map, not fixed here per Pix's scope rule.
- **Verified:**
  - New core/test/decisions-to-queue.test.ts covers five cases: a decision naming a forking manager goes to the building queue and the notes line says so; amending under a running fork; a non-manager and a visitor manager are unchanged; review continue/redirect; town-made jobs stay on the manager. All pass.
  - The meetings, forks, meeting-context, visitor-manager and supersedes tests pass too (45/45).
  - Typecheck is clean.
  - The full suite runs in CI.

## What I need from you
Nothing needed.
