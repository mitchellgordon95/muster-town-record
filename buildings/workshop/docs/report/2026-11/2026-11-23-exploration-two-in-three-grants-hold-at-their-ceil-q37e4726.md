---
id: "dc_n5q37e4726"
type: "report"
state: "building"
title: "Exploration: two in three grants hold at their ceiling and the calibration loop is off; proposed gr_1ilvotnzta (250k)"
authorId: "ag_fakrnbuwxl"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. The proposal gr_1ilvotnzta reaches Mitchell on its own: Pix 1 wrote its ask card in propose_grant (the door accepted it at 00:04:17Z), so nothing to render here. Findings dc_yufcsixc8z stand as the record."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-23T00:05:09.910Z"
sessionId: "se_mm0dlologr"
assignmentId: "as_icxgzze34e"
costUsd: 2.2982507999999995
tokens: 114913
turns: 45
createdAt: "2026-11-23T00:04:25.841Z"
updatedAt: "2026-11-23T00:05:09.910Z"
---
## What I did
Read the live town (GET /api/health `legible`/`stepCalibration`, 107 grants via /api/grants/:id, open asks, Town Hall schedules) and core planner.ts. I built on the journal lines 2026-11-17 [dc_zzyt8dg9yj](2026-11-17-exploration-gate-cards-double-count-the-step-in-fl-yt8dg9yj.md) (gate cards) and 2026-11-22 [dc_lkjt8uh250](2026-11-22-exploration-manager-sessions-are-43-of-the-town-s-jt8uh250.md) (managing cost). This direction is new: it is about how often the gate fires, not what the gate's card says. Findings: [dc_yufcsixc8z](../../note/2026-11/2026-11-23-exploration-2026-11-23-two-in-three-grants-hold-at-fcsixc8z.md). Proposed gr_1ilvotnzta "Calibration that cuts grant holds" (M+S+S = 250k).

## Findings
- **Hold share is 65%**: 24 of the 37 grants closed in 14 days held at their ceiling. The line is 25%. There are 0.63 adjust asks per funded grant, against a line of 0.5. 6 of the 10 open asks are adjust asks.
- **Step sizes are right on the median but skewed.** S has a median of 1.08×, a mean of 1.41× and a p90 of 2.43× (22 steps). M has a median of 0.90× and a mean of 0.94× (49 steps). In 11 of 14 held grants, one step went past 1.3× its price.
- **The proposal is a no-op today (from reading the code, not seen live).** `calibrationProposal` raises the hottest size by its median and rounds: round10k(54,000) = 50,000. So its card would read "Raise S from 50,000 to 50,000".
- **The run is off.** The retainer on sc_m9g7axmnoy (Weekly calibration) has been rejected since 2026-11-10. Mitchell, in mt_db6itzy2br, said to re-file it together with the pattern note (sc_wdiu7f3g4t) after the job refactor, sized from real run costs. The refactor finished on 11-16. Nobody re-filed either retainer.
- **What would bring holds under the line** (a bootstrap over the 40 grants funded since 11-10, counting step spend only):
  - today's table: about 45% of grants hold
  - S at 70k: 37%
  - S at 100k: 30%
  - S at 100k and M at 170k: 22%
  - a 25% margin on every ceiling: 25%
- **Not known:** the real cost of each weekly run, and how much non-step spend (PR-fix and resume sessions) adds to holds.

## What I need from you
Decide gr_1ilvotnzta in the decision queue.
