---
id: "dc_odhmznuk1x"
type: "report"
state: "building"
title: "`open` budget-mode removal proposed as its own grant gr_glon8xr0io (250k) under new dead-code key result kr_ef11f6ex28; Finn on dead-code sweep 1; Nell told"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vie3wrhj54","dc_fpui0p5b1y","dc_anbkv05sk6"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: KR kr_ef11f6ex28 added, gr_glon8xr0io proposed, Finn on dead-code sweep 1. Folded into rollup."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T18:09:04.272Z"
sessionId: "se_470si023c8"
assignmentId: "as_3kpojgg33i"
costUsd: 2.3803617000000004
tokens: 47607
turns: 22
createdAt: "2026-10-28T18:08:44.910Z"
updatedAt: "2026-10-28T18:09:04.272Z"
---
## What I did
- Read Nell's flag inventory [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md) (Mitchell's town-hall mt_m5vub4jd41 decision 3) and our 1:1 notes [dc_fpui0p5b1y](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md) (decision 2: a sixth key result on dead code, flags explicit, the goal-directed flag the named example).
- Re-counted the footprint at main 41236ee: Nell's numbers hold (14 source files read `budgetMode`, 17 test files set it, 7+ docs describe the mode). Site list in my wiki "Dead code".
- Added key result kr_ef11f6ex28 "Unused code paths get found and removed" (sources [dc_fpui0p5b1y](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md), [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md)) to the building goal.
- Proposed gr_glon8xr0io (250,000 tokens) under it: remove the `open` budget mode. Not folded into gr_8ve21typt6 as Nell suggested: that proposal is shared abstractions (kr_doa59kdway), and Mitchell asked for dead-code/flag removal as its own key result, so a standalone proposal is the one he can say yes or no to.
- Assigned Finn dead-code sweep 1 (as_xp8fuautz6, exploration on kr_ef11f6ex28, findings only, ~30–40k): knip/ts-prune triage plus a flags section that cites Nell's note for the building columns and extends it to env/policy/web toggles.
- Cancelled my queued decision-2 assignment as_t57vpubdag (its work, the KR and Finn's sweep, is done here).
- Told Nell (ms_awx3xx9z0m); the town queued it to her as as_izamu57eq0 since it traces to Mitchell.

## Findings
- The removal plan in gr_glon8xr0io: lanes.ts `goalDirected` becomes `kind !== 'town-hall'`; grants.ts (4 sites), prompts.ts (2), entities.ts Town Hall override, ops.ts budget patch, routes/grants.ts, schema PATCH/Create inputs; web Settings select, Places.tsx, keyResults.ts, mock server/sim/fixture; 17 test files lose their `open` cases (one regression test added); 7 docs including invariant 1 of invariants/assignments-lanes.md. The `budgetMode` column stays unread, so no migration; dropping it is a later migration for Mitchell.
- What is lost: the no-gate option for a brand-new building. README already tells new owners buildings are goal-directed, so live behaviour doesn't change for anyone.
- It touches Workshop-owned core/runtime/web code: funding with this scope is the OK to make and merge it; the note invites a counter if Mitchell wants a pre-merge look.
- Three proposals now open for this building: gr_8ve21typt6 (260k), gr_x5gnnmo7yi (150k), gr_glon8xr0io (250k). Finn has one queued; don't start two grants' steps on him at once.
- Spend this session: directed lane (never held by the allowance); exploration today was 172,873 / 828,571 before Finn's sweep.

## What I need from you
Nothing needed from the building; Mitchell decides gr_glon8xr0io in the Town Hall in-tray.
