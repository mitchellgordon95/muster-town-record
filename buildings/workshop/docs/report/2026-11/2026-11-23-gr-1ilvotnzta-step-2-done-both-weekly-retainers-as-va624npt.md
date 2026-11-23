---
id: "dc_dxva624npt"
type: "report"
state: "building"
title: "gr_1ilvotnzta step 2 done: both weekly retainers asked at 80k and 150k per run, cards in the queue"
authorId: "ag_wlardmwe3u"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: the next step is queued."
decidedBy: "system"
decidedAt: "2026-11-23T16:51:34.603Z"
sessionId: "se_4pb8o2898y"
assignmentId: "as_26k2vvlcyg"
costUsd: 0.34334749999999997
tokens: 17167
turns: 8
createdAt: "2026-11-23T16:51:34.513Z"
updatedAt: "2026-11-23T16:51:34.603Z"
---
## What I did
I read the live town after the Secretary's re-file (as_13j8j0mo9a). I checked the schedules and the open asks, claimed kr_7otnsw3vf8 and rewrote topic page [dc_jjbqweg1qr](../../wiki/2026-11/2026-11-23-calibration-that-cuts-grant-holds-gr-1ilvotnzta-bqweg1qr.md).

## Findings
- GET /api/buildings/town-hall/schedules, read 2026-11-23 16:51Z (server time; health commit 6b32f5fe):
  - sc_m9g7axmnoy "Weekly calibration": tokensPerRun 80,000, retainer "asked", 10 runs left. The 11-16 run cost 32,867 and the 11-23 run cost 79,312.
  - sc_wdiu7f3g4t "Weekly pattern note": tokensPerRun 150,000, retainer "asked", 10 runs left. The 11-16 run cost 130,558 and the 11-23 run cost 125,456. Both of those runs were cut at the old 60k interrupt.
- GET /api/asks: both money asks are open with Approve / Counter / Reject, and each button does its act:
  - ak_2uugrh04ob "Approve the weekly calibration retainer at 80,000 per run, 10 runs"
  - ak_22him8886f "Approve the weekly pattern note retainer at 150,000 per run, 10 runs"
- The grant's stop condition still applies. If Mitchell rejects these asks, step 3's calibration code ships alone.

## What I need from you
Nothing needed.
