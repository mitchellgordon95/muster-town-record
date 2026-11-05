---
id: "dc_utyen63g0z"
type: "report"
state: "building"
title: "Half of the last 7 days' spend (62.9M tokens) sits in one \"Not under a grant\" bucket the Bank can't explain; gr_utygatbi85 (300k) would split it by lane and human source"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_aue8kzbaee"],"urls":["https://muster.town/api/finance/spend?window=7d"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_fybzv7we4s"
createdAt: "2026-11-05T00:03:11.849Z"
updatedAt: "2026-11-05T00:03:11.849Z"
---
Live aa6f4fb since 2026-11-04 20:40 UTC. Both funded grants are still held at their checkpoints (your in-tray); this rollup covers one exploration.

## Shipped
**1. A finding, not a feature: the Bank's biggest spend bucket is unreadable**
**What it is:** An exploration read the live 7-day spend. Of 121.8M adjusted tokens, 62.9M (52%) land in "Not under a grant": a flat list of assignment titles (779 rows in Workshop alone) with no lane, no human source and no outcome. Grants are 31.9M (26%), manager sessions 28.1M (23%). Town-wide by lane the same window is directed 34.7M (≈ $772 list), exploration 4.8M (≈ $98), so most of the bucket is work a human asked for, but the page never says so. Findings [dc_k2dzr5cua9](../../note/2026-11/2026-11-05-findings-half-of-the-last-7-days-spend-sits-in-one-dzr5cua9.md); report [dc_aue8kzbaee](2026-11-05-exploration-52-of-7-day-spend-sits-in-an-unexplain-e8kzbaee.md).
**What you'd see:** Bank › Spending › any building › "Not under a grant": a flat title list. No UI change shipped; the data to split it (session/assignment lane, directed sourceId, exploration reservations → proposal) already exists, so no migration is needed.
**Your call:** Fund, counter or reject gr_utygatbi85 (300k; town estimate 178k–339k; 3.79M free under the goal). Funding it is your yes to a Bank display change (it changes nothing the Bank books).

## Decided
- [dc_aue8kzbaee](2026-11-05-exploration-52-of-7-day-spend-sits-in-an-unexplain-e8kzbaee.md) → approve (done; proposal already in your in-tray; nothing queued).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_lwgus14rd2 | kr_pzr1fkgas8 lane × token-kind table | claimed (checkpoint [dc_dxz4r8vifo](2026-11-04-checkpoint-gr-lwgus14rd2-lane-token-kind-table-liv-z4r8vifo.md)) | 734,638 / 600,000 |
| gr_lwgus14rd2 | kr_f49co6lg51 cache-miss alert | on-track (merged 38c3e992, verify held) | " |
| gr_lwgus14rd2 | kr_avafh64h02 manager wakes per building/day | not-started (as_5xuggxsopv waits) | " |
| gr_qggxximtru | kr_au6pcldl3c "Plans paid for" on Inputs | claimed (live 2adb84c2) | 456,488 / 450,000 |
| gr_qggxximtru | kr_ruh7apqptm "Paid in cash, last 30 days" | on-track (merged b39bfdaa, verify as_p2dpcif9qy held) | " |

Spend today by lane: exploration 29,021 tokens; directed 169; grant 0 (both grants held at checkpoint).

## Needs from Mitchell
Nothing needed beyond what is already in your in-tray.

_Already waiting in your in-tray: 1 proposal (gr_utygatbi85), 0 requests, 3 rollups ([dc_mbuiaki9q5](2026-11-04-bank-transparency-spending-now-shows-spend-by-lane-uiaki9q5.md), [dc_dxz4r8vifo](2026-11-04-checkpoint-gr-lwgus14rd2-lane-token-kind-table-liv-z4r8vifo.md), [dc_a6h42ryd7k](2026-11-04-checkpoint-gr-qggxximtru-plans-paid-for-live-on-in-h42ryd7k.md))._
