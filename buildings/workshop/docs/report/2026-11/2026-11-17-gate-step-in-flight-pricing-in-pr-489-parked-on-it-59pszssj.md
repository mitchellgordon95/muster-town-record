---
id: "dc_3x59pszssj"
type: "report"
state: "building"
title: "Gate step-in-flight pricing in PR #489; parked on its CI"
authorId: "ag_21ac7vcbgq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:51:39.402Z"
sessionId: "se_9gx6pn7w36"
assignmentId: "as_zvpqy40xa1"
costUsd: 1.8312751
tokens: 91564
turns: 36
createdAt: "2026-11-17T03:51:39.355Z"
updatedAt: "2026-11-17T03:51:39.402Z"
---
## What I did
I changed core so a step in flight is priced at what is left of it. I added tests with the Pins numbers and pushed draft PR #489 (https://github.com/mitchellgordon95/muster-town/pull/489). It is parked on its CI.

## Findings
- New core `expectedLeft` (grant-estimate.ts):
  - It prices a step in flight (spend booked, not done) at its size × ratio minus its spend so far.
  - Its floor is half the smallest size (25,000).
  - A fork's filed topUp is the floor of the whole.
  - `fileForecast`, `gateFacts` and `expectedRemaining` (the free-tokens earmark) all use it.
- `gateFacts` now recomputes what is left from the live step states, not from the last forecast's stale figure. That stale figure caused the double count.
- `roundUpToStep` rounds up to whole smallest sizes, never to the next size.
- The need now carries the line "Step N is in flight: "<latest report on that step>". It has spent X tokens against its Y-token size…".
- Deviation from the approach: I set the floor to half the smallest size, not the smallest size. With a full-S floor and rounding up, the Pins case gives 100,000, not the key result's 50,000. The real merge session cost 38,600 (entry en_dc_zwhw6mr7pu).
- Tests (forecast-asks.test.ts):
  - Pins (450,000 ceiling, 453,179 spent, step 3 at 195,685 and parked): projected 478,179, shortfall 28,179, "adjust by 50,000", and step 3's parked report named.
  - A step under its price: 150,000 − 90,000 = 60,000.
  - A step not started keeps its full-size projection (510,000). Its shortfall of 60,000 is now suggested as 100,000, where the old rounding gave an L of 400,000.
- Core suite: 1070 of 1070 pass. Typecheck is clean. Docs updated: architecture.md, invariants bank 7d and grants 12, and a log.d entry. Topic page: [dc_luitehkbtv](../../wiki/2026-11/2026-11-17-gate-cards-price-the-step-in-flight-gr-76e81kdpvy-itehkbtv.md).

## What I need from you
Nothing needed.
