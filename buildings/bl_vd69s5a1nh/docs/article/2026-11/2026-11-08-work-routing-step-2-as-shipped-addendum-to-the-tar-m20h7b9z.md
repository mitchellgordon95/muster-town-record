---
id: "dc_wom20h7b9z"
type: "article"
state: "building"
title: "Work routing: step 2 as shipped (addendum to the target model)"
authorId: "ag_i07s9ji4wl"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vxsq9g008a","mt_lsyqj98z0w","as_2vbkchkojc","dc_ktzj41hv8x"],"urls":[]}
tags: ["work-routing","architecture","mt_lsyqj98z0w"]
createdAt: "2026-11-08T04:01:10.086Z"
updatedAt: "2026-11-08T04:01:10.086Z"
---
# Work routing: step 2 as shipped

Addendum to "Work routing: the target model" ([dc_vxsq9g008a](2026-11-08-work-routing-the-target-model-sq9g008a.md); that note is authored by another fork id, so this one carries the step-2 changes). Decided by Mitchell in 1:1 mt_lsyqj98z0w. Assignment as_2vbkchkojc. The PR is linked in the topic page "Work routing" ([dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md)).

## What changed (rows of the 21-path table)

- **Row 10, relay (relayWake):** the recipient is a forking manager → a pending in-tray row, `intrayRow` rule `relay`, one per tell, whatever the manager's status. The human-origin, 3-hop and 24 h gates still apply: a tell with no human origin stays in the inbox only. The `tell` reply carries `intrayRowId`.
- **Row 11, @mention (mentionWake):** → in-tray row, rule `mention` (the live-meeting attendee skip stays).
- **Row 12, outbox answer (requestAnswerWake):** forking manager → in-tray row, rule `request-answer`. A **retired fork's** answer → a directed job on the building queue, chained to the fork's assignment (hole B2 closed).
- **Row 15, grant countered / rejected (`Grants.decisionAssignment`):** → in-tray row, rule `grant-countered` / `grant-rejected`, written for any building manager (not the Town Hall), like continue/adjust/cut. The countered row says how to answer: `propose_grant` with grantId, or `withdraw_grant`.
- **Row 9, the manager's own park:** **no new machinery** (Mara's decision). A park needs a current assignment, and a forking manager never runs a work session now, so it cannot park one. A non-forking manager's park (the Secretary, a lab resident) stays on its own queue. The park simply calls `createAssignment`, which routes it.
- **Row 13, retry:** `managerOnly` is removed. A retry routes like any job: a forking manager's row goes to the building queue.

## The row helper

`intrayRow(world, buildingId, event, {rule, title, what, summary, footer})` in core/src/wakes.ts is the one writer. `managerIntrayRow` now uses it. Each row is a type report, state building, decision pending, authorId system. Its tags are `manager-intray`, `<rule>` and `wake:<rule>:<eventId>:<buildingId>`, written once per event and building. Its `doc.created` event wakes the team-lead session through the existing Waker rule `manager-intray`.

## No work session as a forking manager

- runtime/src/index.ts `scheduleWork` (the `work.residents` loop) skips `isForkingManager(a)`.
- A boot repair, `moveManagerRowsToBuildingQueue` (core domain.ts, called from World boot), moves any pending `queue='agent'` row of a forking manager to the building queue. It writes one `system` event per row with payload.queueRepair, and is idempotent.

## Step 3 (docs) still open

These docs are stale until step 3:
- architecture.md: :22, :31-52, :56-57, :98, :278, :289-291
- docs/wakes.md: §4 step 2 and step 3 history text (:140-150), :34, :41
- invariants/assignments-lanes.md: inv. 7–8
- how-work-gets-done §6
- prompts.ts:206
- AGENTS.md non-negotiable 1, and team-lead prompt C1

Already fixed in step 2: docs/wakes.md table row for `grant.countered`/`grant.rejected`, goal-directed-budgets.md (counter/reject), invariants/grants.md "Decisions → assignments".

