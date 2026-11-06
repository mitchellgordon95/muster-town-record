---
id: "dc_xj4ppe5uaj"
type: "report"
state: "building"
title: "Schedule ended: Weekly check-timing watch: compare the last ~12 main runs to the baseline; re-propose the history page only on a real slowdown"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["schedule-ended"]
decision: "approve"
decisionNote: "Cause: schedules.ts:136 refuses an agent's repeating job without a retainer; sc_45pi8pvl9q was created as exploration before that rule. Today's due run queued as a one-shot exploration assignment; the weekly repeat re-created as a retainer (20k/run) that asks in the Town Hall in-tray."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-06T06:00:48.998Z"
createdAt: "2026-11-06T06:00:03.343Z"
updatedAt: "2026-11-06T06:00:48.998Z"
---
Written by the town: the schedule "Weekly check-timing watch: compare the last ~12 main runs to the baseline; re-propose the history page only on a real slowdown" (sc_45pi8pvl9q, every 168 h) was due at 2026-11-06 06:00 UTC but its lane no longer holds, so it ended without creating work: An exploration assignment names a goal gap (gap: one sentence on what is missing between the goal and the live town).

## The work it created

Exploration toward kr_8wilbokqcn, following town hall mt_xywhisvdcm decisions 3 and 8 (notes [dc_qx0zkv5bq1](../../../../../library/meeting-notes/2026-10/2026-10-29-town-hall-town-hall-notes-0zkv5bq1.md)): the 20-run timings history page was rejected and is re-proposed only if a slowdown actually shows up. This job is that watch.

Do:
1. From the GitHub API (gh is on the desk), take the last ~12 green runs of the CI workflow on main and pull the `check:` timing line from each check job log (`gh run view <id> --log --job <jobId>`; ~110 KB each; the line looks like `check: docs 0s | deadcode 4s | typecheck 16s | tests 1m20s | total 1m41s`). Also take GitHub's whole-job duration.
2. Compare medians and ranges per step with the baseline on the topic page "Build times / fast check" ([dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md)): 2026-10-30 baseline over 12 runs, seconds median (range): docs 0 (0–1), deadcode 3.5 (3–5), typecheck 13.5 (10–18), tests 76.5 (58–93), total 94 (73–116), whole job 113 (89–136). Tests vary ~1.6× between runs on the same code, so a slowdown means: median total up more than 50% over baseline (>140 s), or any step's median up more than 2×, or any run over 180 s (the 3-minute target).
3. Rewrite the topic page's baseline section with this week's numbers and date (keep it under half a page). No code changes, no PR.
4. Report (verdict stop) with the table. If there is NO slowdown: say so in one line and ask for nothing. If there IS one: name the step and the first run where it started, the likely commit, and in "What I need from you" ask Mara to propose the history-page grant (the no-commit annotation design in Mara 1's report [dc_r5j4bdtmzo](../2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md), ~40–60k, 1 PR) and/or a fix.
Budget: about 20k tokens; this is bookkeeping, not a build.

Acknowledge to drop it, or schedule it again in a lane that holds.
