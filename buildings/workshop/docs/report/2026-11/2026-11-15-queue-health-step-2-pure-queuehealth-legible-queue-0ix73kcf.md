---
id: "dc_pl0ix73kcf"
type: "report"
state: "building"
title: "Queue health step 2: pure queueHealth + legible.queue + rank-run block, PR #460 open, parked on CI"
authorId: "ag_2d6yc3kbil"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T21:59:40.997Z"
sessionId: "se_z2bvjl3kq4"
assignmentId: "as_kjgoqq0edx"
costUsd: 1.779067
tokens: 88953
turns: 36
createdAt: "2026-11-15T21:59:40.982Z"
updatedAt: "2026-11-15T21:59:40.997Z"
---
## What I did
Wrote the pure `queueHealth` function with seeded property tests, fed it into `legible.queue` on /api/health, and appended a Queue health block to the Secretary's rank run. Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/460. Parked on its CI.

## Findings
- **New file `packages/core/src/queue-health.ts`.** `queueHealth(input, now)` takes plain arrays and never touches World. For each ask type over 14 days it gives medians, each with its sample size:
  - decision hours: from creation to a human decision. A retire counts only when its `by` is a us_ id.
  - minutes on card: the union of the decider's capped views on the ask or on its target, clipped to the span from creation to decision. Overlapping views count once, so this never exceeds decision time.
  - first seen to decision, in minutes.
  - clarifying lines: the decider's 1:1 lines said inside one of those views, in the same meeting, and how many end in "?".
- **Gates and budget.** For each grant funded in the window, gates = the larger of its checkpoint holds and its adjust asks. A hold files its adjust ask, so this counts each gate once. Hold share today = grants at a gate ÷ live grants. Budget used = Σspent ÷ Σgranted. The warning fires when gates per grant < `FEW_GATES_PER_GRANT` (0.5) and budget used > `HIGH_BUDGET_USED` (0.85). Both thresholds are assumptions for Mitchell to tune in step 4.
- **Wiring.** `measures.ts` builds the input from the db and adds `legible.queue`. `secretary.ts` `rankRunText` appends "## Queue health, last 14 days" to the rank run, both when the schedule fires (schedules.ts) and on "Rank now".
- **Tests.** `test/queue-health.test.ts` runs 5 properties over 200 seeded random towns each: time on card ≤ decision time; a line outside every view never counts; adding a view never lowers time on card; budget used = spent ÷ granted and never negative; every median has a sample. Three example tests cover an empty town returning nulls, a worked money ask (20 min on card, 2 lines, 1 question, warning on) and a human retire vs a system retire. measures.test and secretary.test also check the new fields.
- **Local check.** `npm run check --fast` passes: docs, knip, typecheck and tests (8m11s).
- **Design choice.** Card time, first seen and lines are taken only over asks seen at least once in the queue, so asks decided elsewhere don't pull the medians to 0. The topic page [dc_271txc8zem](../../wiki/2026-11/2026-11-12-queue-health-gr-pdja05z2f1-1txc8zem.md) has the detail.

## What I need from you
Nothing needed.
