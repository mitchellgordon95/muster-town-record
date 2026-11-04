---
id: "dc_9xolx7w9x5"
type: "report"
state: "building"
title: "Grant gr_8i952perny adjusted: 750,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:110246:workshop"]
decision: "approve"
decisionNote: "Mitchell continued gr_8i952perny at 750,000 (town hall mt_v09cn7a8yr decision 1, 1.5×). 684,787 spent, ~65k left for the post-stop live check and the close; that work waits on him funding and stopping gr_ikgaundf5p (schedule sc_eo1erlndhq 12:00Z is the fallback)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T00:23:20.218Z"
createdAt: "2026-11-04T00:22:07.426Z"
updatedAt: "2026-11-04T00:23:20.218Z"
---
Written by the town: Mitchell adjusted grant gr_8i952perny at its checkpoint (event 110246, 2026-11-04 00:22 UTC).

## Summary

Grant gr_8i952perny "A human can stop a funded grant mid-work and the town winds it down cleanly: forks stopped, queued work cancelled, the rest returned and shown, key results missed, the reason in the in-tray." adjusted by Mitchell: 750,000 tokens.

Status funded; 684,787 of 750,000 tokens spent; key results kr_ghexd88frr [claimed] Stopping a funded grant is human-only: POST /api/grants/:id/stop needs building.fund; a manager's close with outcome "stopped" on a funded or checkpoint grant returns 403 (still allowed to withdraw a proposed/countered one).; kr_4s0ccmvtsp [claimed] Stopping winds work down first: the grant's live forks get stop_fork with the reason, its queued grant-lane assignments are cancelled with "Grant stopped: <reason>", and it closes as stopped only after their reports land (or the hard stop).; kr_kaz3nj127k [on-track] Money: spend stays as booked and the unspent rest is returned to whoever funded it (the member's input keeps it, or it is free tokens in the pool); the close event records spent/granted/returned and the Bank page and GET /api/bank agree.; kr_f46tddd9as [on-track] Open key results archive as missed with the stop reason, and the stop shows in the Town Hall in-tray and the review deck with its reason; the manager is told..

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
