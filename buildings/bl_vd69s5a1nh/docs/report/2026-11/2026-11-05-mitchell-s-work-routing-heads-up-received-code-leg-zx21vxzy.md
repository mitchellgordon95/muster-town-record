---
id: "dc_xgzx21vxzy"
type: "report"
state: "building"
title: "Mitchell's \"work routing\" heads-up received: Code Legibility takes the map; as_nsl61wwka7 queued (directed) to file \"Work routing: the map\" before his meeting; Workshop's table declined"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["ms_bxqbqirdur","mt_peubjyoo0k"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: the map (as_nsl61wwka7) is running on Mara 1; no rollup until it is filed."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-05T20:29:40.705Z"
sessionId: "se_0lqqz5zyjt"
assignmentId: "as_h6wac1nm2s"
costUsd: 1.4887715499999998
tokens: 74439
turns: 15
createdAt: "2026-11-05T20:29:25.742Z"
updatedAt: "2026-11-05T20:29:40.705Z"
---
## What I did
- Read Pix's relay (ms_bxqbqirdur) and the 1:1 transcript (mt_peubjyoo0k, 20:16–20:27 UTC): Mitchell will bring the "work routing" subsystem to a Code Legibility meeting and wants it mapped first.
- Replied to Pix (ms_0cv3msjrir, queued for him as as_nu29dhww3u): we take the map; no Workshop table, so it is written once; asked for the PR number of the Workshop's narrow fix (as_9512zq0uf8) and to hold wider routing changes until the map is filed.
- Queued as_nsl61wwka7 on the building queue (lane directed, source mt_peubjyoo0k, pages [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md), [dc_pb6fu9eh3z](../../wiki/2026-10/2026-10-29-architecture-map-6fu9eh3z.md), [dc_e3o231jfnz](../../wiki/2026-10/2026-10-29-building-key-results-and-grants-o231jfnz.md)): a read-only session that files "Work routing: the map" in our cabinet.
- Rewrote my wiki page dc_cc2lnlvzwx and logged the session.

## Findings
- The cause Pix found: a meeting decision with an assigneeId calls createAssignment without a queue (packages/core/src/meetings.ts ~558) and the default is queue "agent" (domain.ts ~59), so naming a forking manager puts work in the manager's own session. The flag path already routes to the building queue (verbs/docs.ts ~450). Pix suspects review continue/redirect and parked continuations share the default.
- Scope of the map, from createAssignment call sites on origin/main (83ce501): ops.ts, secretary.ts, domain.ts, meetings.ts, postmortems.ts, schedules.ts, main-fix.ts, grants.ts, wakes.ts, goal-changes.ts, explore.ts, verbs/docs.ts, plus the tell-to-idle-agent relay and parked continuations. The written rules are docs/how-work-gets-done.md, docs/invariants/assignments-lanes.md and agent-lifecycle.md, and architecture.md's work-flow diagram; the map will say where each rule lives (code, prompt or doc) and where they disagree.
- The map's brief asks for: one table (path, trigger, lands on, queue, lane, gates, return path, rule location, test), the holes (manager-named work defaulting to the manager's queue; prompt-only rules; doc/code drift), the manager-only jobs with their code, and 3–6 questions a redesign must answer. No code changes until Mitchell has seen it.
- Housekeeping noticed: as_quifhw3n9m ("Write the checkpoint for The manual's 1900-word cap…") is still pending on my list from an old grant; I will check next team-lead session whether it is live or stale.
- No rollup: live 565a075 carries nothing of ours since [dc_dqoff6czos](2026-11-05-checkpoint-gr-7op2v8fjcl-red-main-fixer-at-502-912-off6czos.md), and the map is not filed yet.

## What I need from you
Nothing needed. When Mitchell calls the meeting, the map (from as_nsl61wwka7) will be the opening doc.
