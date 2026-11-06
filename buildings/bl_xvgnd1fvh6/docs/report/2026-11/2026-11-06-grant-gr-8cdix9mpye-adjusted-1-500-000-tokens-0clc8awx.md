---
id: "dc_ig0clc8awx"
type: "report"
state: "building"
title: "Grant gr_8cdix9mpye adjusted: 1,500,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:137280:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: gr_8cdix9mpye now 1,500,000 (383,248 spent). Step 3a queued on the building queue (SSRF live check + a well-known proof from a static host the town can make itself); the real self-host town (kr_89cb8eda84) still waits on outbox dc_nke6xw12k4."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:34:26.260Z"
createdAt: "2026-11-06T04:31:37.169Z"
updatedAt: "2026-11-06T04:34:26.260Z"
---
Written by the town: Mitchell adjusted grant gr_8cdix9mpye at its checkpoint (event 137280, 2026-11-06 04:31 UTC).

## Summary

Grant gr_8cdix9mpye "Strangers register a self-hosted town with muster.town's directory by DNS name, prove control with a TXT record or a well-known URL, and appear in GET /api/directory with no account and no approval." adjusted by Mitchell: 1,500,000 tokens.

Status funded; 383,248 of 1,500,000 tokens spent; key results kr_og03nxrkct [not-started] Directory registration, no approval and no account (Prod): POST /api/directory/register takes a DNS name and returns a token; control is proven by a TXT record at _muster-town.<host> or GET https://<host>/.well-known/muster-town carrying it; one entry per host; dropping the proof delists.; kr_a7f8a181a6 [not-started] Step 1: register and list shape live on muster.town; kr_dc79c27ff0 [not-started] Step 2: a throwaway fly.dev app serving the token is verified, listed, and delisted when the proof is removed; kr_7c07b8826c [not-started] Step 2: private and Fly-internal addresses are never fetched; kr_89cb8eda84 [not-started] Step 3: a stranger-style town from docs/self-host.md is listed.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
