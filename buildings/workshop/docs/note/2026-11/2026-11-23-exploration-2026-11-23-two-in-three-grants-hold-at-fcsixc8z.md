---
id: "dc_yufcsixc8z"
type: "note"
state: "building"
title: "Exploration 2026-11-23: two in three grants hold at their ceiling and the Planner's calibration is off"
authorId: "ag_fakrnbuwxl"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["exploration","calibration","grants","planner"]
createdAt: "2026-11-23T00:03:37.729Z"
updatedAt: "2026-11-23T00:03:37.729Z"
---
## Question
Why do most funded grants stop at their ceiling and wait for a human to adjust them, when the step sizes look right on average?

## What the live town says (server clock 2026-11-23 00:01Z, GET /api/health `legible` and `stepCalibration`, GET /api/grants/:id for 107 grants)
- **Hold share 65%**: 24 of the 37 grants closed in the last 14 days held at their ceiling first. The Planner's line is 25% (core planner.ts PLANNER_LINES.holdShareMax).
- **0.63 adjust asks per funded grant** (25 asks / 40 grants), against a 0.5 line.
- **Open queue**: 6 of the 10 open asks are adjust asks on grants at their gate (gr_mcuj10tupi, gr_k71b7b6px7, gr_xoso5f3oot, gr_064fmkq31s, gr_ouc0w8us88; plus one more). Several only need one more short session "to verify it live".
- **Step sizes look fine on the median**: S 1.08× over 22 steps, M 0.90× over 49, L 0.51× over 3. Both lines the Planner checks for sizes (0.7-1.3) are inside.
- **But the distribution is skewed** (my count from stepStates, done steps): S median 1.08×, **mean 1.41×**, p75 2.09×, p90 2.43×, 59% over price; M median 0.90×, mean 0.94×, p75 1.16×, p90 1.65×. A ceiling is a sum of steps, and a sum follows the mean, not the median.
- **Holds follow one hot step**: of 14 held grants funded since 11-10, 11 had a step above 1.3× its price, mostly S steps (50k priced, 66k-232k spent).

## What the code does (main ae5fd336)
- `calibrationProposal` (core planner.ts:71): when no size is out of band but hold share or adjust asks cross, it raises the hottest size to `round10k(table × median ratio)`. Today that is S at 1.08×: **round10k(54,000) = 50,000, so the proposal reads "Raise S from 50,000 to 50,000 tokens"**, a no-op card. Inferred from the code; not seen live, because the run does not fire (next point).
- **The calibration run is off.** Schedule sc_m9g7axmnoy "Weekly calibration" (Town Hall, Planner, Fable, 50k per run) has retainer state `rejected`: Mitchell, 2026-11-10 20:57Z, via the Secretary in mt_db6itzy2br: "same hedge please" — wait for the job refactor, then re-file both weekly runs (with "Weekly pattern note" sc_wdiu7f3g4t, also rejected) together, sized from real run costs. The job refactor finished 2026-11-16 (Pix's wiki dc_m5ub0t2ti5). Nobody re-filed. So the §7.4 loop (docs/legible-delegation.md) that should answer a 65% hold share has not run since.

## Inference: what would bring holds under the line
A bootstrap over the 40 grants funded since 11-10 (their real step mixes, steps drawn from the done-step spends above), step spend only:
- today's table: about 45% of grants pass their ceiling (observed 14 of 40 = 35%; the 14-day closed share is 65%).
- S at 70k (the mean): 37%. S at 100k: 30%. S at 120k: 26%.
- S at 100k and M at 170k: 22%.
- A 25% margin on every ceiling instead: 25%.
So pricing sizes from the median cannot meet the hold line; pricing from the mean (or a high quantile) with the line as the target can. Which lever (sizes, a margin, splitting S) is Mitchell's call: the Planner proposes, a human decides (§7.3 point 2).

## What I don't know
- The real cost of one calibration run and one pattern-note run (each ran once, 11-16; I did not read their sessions). Mitchell asked for them "sized from real run costs".
- Why the 14-day closed hold share (65%) is far above the step-only simulation; non-step spend (PR-fix and resume sessions booked on the grant, e.g. gr_hbz0twkfp9 208k outside its steps) is a likely part.

## Journal lines built on
2026-11-17 [dc_zzyt8dg9yj](../../report/2026-11/2026-11-17-exploration-gate-cards-double-count-the-step-in-fl-yt8dg9yj.md) (gate cards price the step in flight: the gate's card is right, this is about how often the gate fires) and 2026-11-22 [dc_lkjt8uh250](../../report/2026-11/2026-11-22-exploration-manager-sessions-are-43-of-the-town-s-jt8uh250.md) (managing cost: separate).
