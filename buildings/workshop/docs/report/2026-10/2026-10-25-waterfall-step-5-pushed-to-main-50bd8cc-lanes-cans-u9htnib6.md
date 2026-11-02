---
id: "dc_8du9htnib6"
type: "report"
state: "building"
title: "Waterfall step 5 pushed to main (50bd8cc): lanes, canStart gate, 50%/100% checkpoints, propose_grant/checkpoint_grant, Key results brief"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 5 accepted as built (50bd8cc). The live check and step 6 go out as separate assignments."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T04:27:44.829Z"
sessionId: "se_hwej1uuspz"
assignmentId: "as_kfq4p6kbeh"
costUsd: 5.2063291000000005
tokens: 249178
turns: 87
createdAt: "2026-10-25T00:27:19.522Z"
updatedAt: "2026-10-25T04:27:44.829Z"
---
## What I did
I checked processes at the start: there was only one claude process, so nothing to kill. The fcef26c live check was already closed in [dc_wwap0nwddl](2026-10-24-town-hall-in-tray-badge-verified-on-live-867dc3f-i-ap0nwddl.md). An earlier session had left part of step 5 uncommitted in my checkout (schema, lanes.ts, policy.ts, gate, checkpoint logic), probably cut off by a redeploy. I finished it, tested it and committed straight to main as **50bd8cc**, then queued a redeploy. **50bd8cc should be live** after the restart; I'll check it next session.

## Findings
What each of the five parts looks like in code:
1. **Lanes.**
   - Migration `030_assignment_lanes.sql` (030 was the next free number) adds lane, grantId, keyResultId, gap and heldReason to assignments. The DROP line is added in v12.test.ts.
   - `ops.startSession` copies lane and grantId from the assignment onto the session.
   - The `assign` verb and `POST /api/agents/:id/work` (WorkInput) take the lane fields. `resolveLane` (core/src/lanes.ts) checks them:
     - exploration needs a keyResultId or a gap;
     - grant needs a grantId plus a keyResultId of that grant, and the grant can't be draft, closed or rejected.
   - Only in goal-directed buildings: agents can't create directed work. Humans, the system and meeting decisions still can.
   - With no lane fields, a continuation takes the lane of the work it continues; anything else is directed.
   - Open buildings behave as before.
2. **Gate.**
   - `Budget.canStart(agentId, assignment?)` adds `laneHold`:
     - grant: the grant must be funded (the checkpoint assignment itself may also run while its grant is at checkpoint);
     - exploration: the building's spend today must be under its allowance;
     - directed: no extra check.
   - A held assignment stays pending with `heldReason` set, e.g. "held: grant at checkpoint". Nothing is cancelled.
   - The scheduler and the redeploy "blocked" list use the new `nextStartable`, which skips held work so work queued behind it still starts. `preflightWork` checks the gate too.
3. **Checkpoint.**
   - After every charge (`Budget.recordUsage` → `afterCharge` → `Grants.checkpoints`), a funded grant whose spend from sessions crosses 50% or 100% fires once per fraction:
     - status becomes checkpoint and `checkpointsDone` records the fraction;
     - a `grant.checkpoint` event is appended;
     - humans who can fund get an inbox note;
     - the manager agent gets "Write the checkpoint for <objective>" at the front of its queue (lane grant, no key result, created by the system).
   - New `checkpoint_grant` verb {grantId, reportId?, keyResults:[{id,status,note}]} sets key-result statuses up to claimed (met and missed are refused).
   - `reportId` is optional because `submit_report` ends the session, so the manager can't file the report first and then call the verb. Instead, a `rollup:true` from a checkpoint assignment links itself (`checkpointDocId`), is tagged rollup and checkpoint, doesn't need sourceIds, and lands in the Town Hall in-tray.
4. **Prompts.**
   - In goal-directed buildings, `keyResultsBlock` goes right after "Building goal:" in both the desk brief and host sessions. It shows each funded or checkpoint grant (objective, spend / grant tokens), its key results with status and how-to-check, today's exploration against the allowance, any open proposal, and this session's lane ("This session: exploration on gap: …").
   - The manager gets a "## Grants" block covering assign lanes, `propose_grant` (new: create and propose in one call, one open proposal per building) and `checkpoint_grant`.
5. **Open questions as settings.** `core/src/policy.ts` has a `BUDGET_POLICY` constant for each:
   - explorationShare 0.1, plus explorationSplitAcrossPool false;
   - directedBypassesGrants true;
   - funders "managers-and-admins" (never agents);
   - grantReservations false (grants are ceilings).

   Each of Mitchell's answers is a one-line change there.

**Tests:**
- New `core/test/lanes.test.ts`: 10 of 10 pass.
- Full core suite: 246 of 247. The one failure is the memory.test.ts log test; it passes when run alone and nothing in this change touches it, so it looks like a timeout under load.
- Typecheck: the whole repo passed before I rebased onto main; after the rebase, the runtime tsc (which also compiles core and schema) is clean.
- Runtime tests were not run.

Worth knowing: when a pool has no daily inflow, the default exploration allowance is 0 and all exploration is held. Live should be fine (the design note puts the inflow at about 20M tokens/day), but worth a check when step 7 flips the pilot.

## What I need from you
Nothing needed.
