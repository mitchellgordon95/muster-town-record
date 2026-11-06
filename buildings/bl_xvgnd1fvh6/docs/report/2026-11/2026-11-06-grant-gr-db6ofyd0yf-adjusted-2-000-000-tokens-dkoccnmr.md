---
id: "dc_4sdkoccnmr"
type: "report"
state: "building"
title: "Grant gr_db6ofyd0yf adjusted: 2,000,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:136103:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: Mitchell adjusted gr_db6ofyd0yf to 2,000,000 tokens at its checkpoint (863,216 spent). The lane gate re-checks the grant's status each tick (core/src/lanes.ts:126-135), so grant work runs again. The 2-day-old continuation as_vv75lxz36e is replaced by a fresh step-3 assignment with the current state (PR #340 is stale against main acda269 and touches Bank read paths; the top-up is the go-ahead rollup #36 asked for)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:16:50.355Z"
createdAt: "2026-11-06T04:15:50.052Z"
updatedAt: "2026-11-06T04:16:50.355Z"
---
Written by the town: Mitchell adjusted grant gr_db6ofyd0yf at its checkpoint (event 136103, 2026-11-06 04:15 UTC).

## Summary

Grant gr_db6ofyd0yf "Halve muster.town's runtime tick (live ~200 ms, 856 ms after boot) by stopping it from recomputing Bank.expectedSession and debit sums on every call, so tick p95 stays under 500 ms well past 1.5× today's world." adjusted by Mitchell: 2,000,000 tokens.

Status funded; 863,216 of 2,000,000 tokens spent; key results kr_0cbw6jb2p8 [at-risk] Live tick roughly halved: muster.town's runtime tick median is under 110 ms, and the streams phase is under 10 ms; kr_50wtkdofgc [on-track] Desk headroom: tick p95 at 2× the live world is ≤ 250 ms and at 4× ≤ 900 ms, recorded in docs/scaling.md; kr_2djaq46ga6 [claimed] No Bank number moves: tests pin that expectedSession, Bank.available and freeTokensAll give the same outputs with the caches, and that a session ending invalidates the cache.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
