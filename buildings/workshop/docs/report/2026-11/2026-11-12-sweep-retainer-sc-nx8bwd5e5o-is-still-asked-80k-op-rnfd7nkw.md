---
id: "dc_ndrnfd7nkw"
type: "report"
state: "building"
title: "Sweep retainer sc_nx8bwd5e5o is still \"asked\" (80k open in the Town Hall); today's 19:00Z run will fire and be held"
authorId: "ag_xvgyj5ia74"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Read-only check done: Mitchell's decline of ak_8kd7c0ab44 (click, on kr_hee2pa2d5r) did not touch sc_nx8bwd5e5o; its 80k retainer ask ak_4r86pl1jz0 is open in the Town Hall. Today's 19:00Z run fires and is held, not skipped (schedules.ts:243, retainers.ts:238-240). No code change, nothing to queue. The ask has its own in-tray row, so no Needs line."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T15:24:35.331Z"
sessionId: "se_sq2j03rled"
assignmentId: "as_ejcnht75kd"
costUsd: 0.5779872
tokens: 28899
turns: 14
createdAt: "2026-11-12T15:24:23.003Z"
updatedAt: "2026-11-12T15:24:35.331Z"
---
## What I did
I made read-only calls with the desk bearer. Live was 7be84c3c (health at 15:23:42Z). I read GET /api/buildings/workshop/schedules, /api/asks/ak_8kd7c0ab44, /api/asks, /api/assignments/as_yi9bl73x23, and /api/events?from=15:00Z (813 events up to 15:23:56Z). I then checked the result against lanes.ts, retainers.ts and schedules.ts. I edited nothing, made no PR and re-asked nothing.

## Findings
**1. Schedule sc_nx8bwd5e5o, "Onboarding staleness sweep":**
- retainer **asked**
- retainerTokens 312,312: the old approved total, still stored
- drawnTokens 182,132, claimTokens 0
- tokensPerRun 20,000, runsLeft 4, askTokens **80,000**
- nextRunAt 2026-11-12T19:00:00Z, endsAt 2026-11-15T23:59:59Z, paused false, status active, runs 8
- retainerNote null
- retainerDecidedAt 2026-11-10T17:35:35.954Z, by us_1la74k332n (that was the earlier approval)
- updatedAt 2026-11-11T19:08:45Z: your 11-11 edit re-asked it
- The last run, as_yi9bl73x23 (11-11 19:00Z), is **done**.

**2. Ask ak_8kd7c0ab44:**
- type **click**, targetKind **keyResult**, targetId **kr_hee2pa2d5r**. It does not target the schedule.
- Branches are Done and Decline. It came from [dc_y3pqu4tfip](2026-11-07-rollup-52-onboarding-sweep-10-live-manual-fixed-th-pqu4tfip.md) and was created 11-09 04:05Z.
- Mitchell decided **"Decline"** at 15:14:48.460Z, with no note.
- So the decline cannot touch sc_nx8bwd5e5o.
- There is a separate open ask: **ak_4r86pl1jz0**, money / retainer / sc_nx8bwd5e5o, "Approve the retainer for "Onboarding staleness sweep" at 80k", created 2026-11-11T19:08:45Z, status open. It is 1 of 31 open asks.

**3. Events since 15:00Z:**
- There are **no retainer.\* events** and no schedule.\* events for sc_nx8bwd5e5o.
- The only ask event about the schedule is `ask.decided` at 15:14:48Z, "Decided "Approve the 320k retainer…": Decline". Nothing on ak_4r86pl1jz0.

**4. Today's 19:00Z run will fire and then be held, not skipped.** This is how the code handles it:
- fireSchedules (schedules.ts:243): the schedule is active, not paused, and nextRunAt is before endsAt. The last assignment is done, so it is not skipped as "still queued". The missed-run branch only applies when `retainer === "funded"`, so it does not apply here. calibrationIdleReason returns null for a schedule that is not the Planner's.
- So it calls createAssignment with lane retainer and createdBy system. That passes lanes.ts:81-85. It creates the assignment and logs `schedule.fired`.
- The lane gate (lanes.ts:139-142 → retainerHold, retainers.ts:238-240) then holds the assignment with **"held: retainer not approved (asked)"**.
- It stays queued until ak_4r86pl1jz0 is approved.
- While it is queued, each later daily fire is logged as `schedule.skipped` ("its last assignment is still queued"), and no second run piles up.
- If Mitchell approves the 80k before 19:00Z, today's run runs normally.

## What I need from you
Nothing needed. Whether to ask Mitchell about ak_4r86pl1jz0 before 19:00Z is your call; nothing changes in the code either way.
