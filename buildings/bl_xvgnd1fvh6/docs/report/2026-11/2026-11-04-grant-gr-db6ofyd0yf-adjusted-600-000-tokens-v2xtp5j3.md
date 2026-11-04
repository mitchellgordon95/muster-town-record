---
id: "dc_aqv2xtp5j3"
type: "report"
state: "building"
title: "Grant gr_db6ofyd0yf adjusted: 600,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:115958:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: Mitchell topped gr_db6ofyd0yf up to 600,000 (445,885 spent). The hold lifted by itself: as_fo0a9tdu70 (PR #304 merge on green) started on Cleo 1 at 17:16:44Z. Step 3 queued behind it."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T17:17:01.072Z"
createdAt: "2026-11-04T17:16:39.990Z"
updatedAt: "2026-11-04T17:17:01.072Z"
---
Written by the town: Mitchell adjusted grant gr_db6ofyd0yf at its checkpoint (event 115958, 2026-11-04 17:16 UTC).

## Summary

Grant gr_db6ofyd0yf "Halve muster.town's runtime tick (live ~200 ms, 856 ms after boot) by stopping it from recomputing Bank.expectedSession and debit sums on every call, so tick p95 stays under 500 ms well past 1.5× today's world." adjusted by Mitchell: 600,000 tokens.

Status funded; 445,885 of 600,000 tokens spent; key results kr_0cbw6jb2p8 [on-track] Live tick roughly halved: muster.town's runtime tick median is under 110 ms, and the streams phase is under 10 ms; kr_50wtkdofgc [not-started] Desk headroom: tick p95 at 2× the live world is ≤ 250 ms and at 4× ≤ 900 ms, recorded in docs/scaling.md; kr_2djaq46ga6 [claimed] No Bank number moves: tests pin that expectedSession, Bank.available and freeTokensAll give the same outputs with the caches, and that a session ending invalidates the cache.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
