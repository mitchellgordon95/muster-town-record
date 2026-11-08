---
id: "dc_u3d8g27k38"
type: "report"
state: "building"
title: "Work routing step 3: docs PR #396 opened; parked on CI"
authorId: "ag_gtu44wswoz"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Good recovery of the stashed edits and the two text corrections. Continuation as_yd25ug53x3 (merge #396 if green) is already waiting on {pr: 396}; nothing more to queue."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-08T04:23:13.715Z"
sessionId: "se_32tvsc0akx"
assignmentId: "as_y1p4s1e225"
costUsd: 0.5534373
tokens: 27672
turns: 16
createdAt: "2026-11-08T04:22:41.112Z"
updatedAt: "2026-11-08T04:23:13.715Z"
---
## What I did
I found the first try's edits auto-stashed on the desk and applied them. I checked each claim against the code at 5f6571f5 and fixed two lines. Then I committed, pushed and opened draft PR #396 (https://github.com/mitchellgordon95/muster-town/pull/396).

## Findings
- **Files changed (14):** AGENTS.md (non-negotiable 1), docs/architecture.md, docs/wakes.md (a "since work routing" note, the inventory rows for tell / mention / request-answer / blocked, history notes), docs/how-work-gets-done.md, docs/invariants/assignments-lanes.md (invariant 8 and a new invariant 9, which cites its 7 tests), docs/log.md, packages/core/src/prompts.ts (team-lead text and review-flag text), memory.ts (manager text), verbs/docs.ts and schema/src/index.ts (assign descriptions), domain.ts (error text), runtime index.ts and manage.ts (comments), test/prompts.test.ts.
- **What the docs now say:** a forking manager never runs a work session. A job that names it goes on the building queue. A tell, @mention, outbox answer, or grant counter/reject that reaches it becomes a pending in-tray row (`intrayRow` / `relayWake`).
- **Checks:**
  - All 7 tests cited in invariant 9 exist under those exact names.
  - `moveManagerRowsToBuildingQueue`, `intrayRow` and `isForkingManager` exist at the places the docs name.
- **Two fixes to the first try's text:**
  - I dropped "with your redeploy and Town Hall board permissions": I could not confirm that forks have Town Hall board permissions.
  - The review prompt no longer says assigneeId is "for yourself".
- **Local runs:** typecheck ok. prompts, work-routing-step2, wakes, decisions-to-queue and lanes tests: 55/55 pass. check:docs ok (manual.md is at 1898/1900 words, untouched). knip clean.

## What I need from you
Nothing needed. The next session merges #396 if CI is green.
