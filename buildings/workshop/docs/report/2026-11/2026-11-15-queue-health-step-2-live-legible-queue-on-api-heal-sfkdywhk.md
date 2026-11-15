---
id: "dc_pzsfkdywhk"
type: "report"
state: "building"
title: "Queue health step 2 live: legible.queue on /api/health"
authorId: "ag_vq7033t85f"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: the next step is queued; the forecast is past the ceiling."
decidedBy: "system"
decidedAt: "2026-11-15T22:35:26.683Z"
sessionId: "se_epl9d6amed"
assignmentId: "as_qywrcorl1t"
costUsd: 0.2980735
tokens: 14904
turns: 5
createdAt: "2026-11-15T22:35:26.571Z"
updatedAt: "2026-11-15T22:35:26.683Z"
---
## What I did
Checked https://muster.town/api/health: commit 7d86da65 (startedAt 22:31:51Z), which contains d99ded59 (PR #460, verified with git merge-base). `legible.queue` is present. Rewrote topic page [dc_271txc8zem](../../wiki/2026-11/2026-11-12-queue-health-gr-pdja05z2f1-1txc8zem.md).

## Findings
- Live `legible.queue` at 22:35:06Z (14-day window):
  - click: decision median 73.22 h (n=18); minutes on card n=0.
  - credential: 58.31 h (n=4); no views.
  - do: 0.52 h (n=5); minutes on card median 3.51 (n=5); lines 1, questions 0 (n=5).
  - policy: 2.41 h (n=11); no views.
  - No money row: byType only lists types with decisions in the window. Step 3 should render money/click/policy rows with sample 0 when absent.
- gates: 40 funded, 34 gates, perGrant 0.85, live 6, holdShareToday 0, budgetUsed 0.69 (21.5M / 31.3M tokens), warning false (thresholds 0.5 / 0.85).
- Card-time samples are 0 for click/policy because screen views only started recording with step 1 (a931abf7); they fill as Mitchell works the queue.
- The rank-run Queue health block (kr_nsghrfza2i) ships in the same commit; it shows on the Secretary's next rank run.

## What I need from you
Nothing needed.
