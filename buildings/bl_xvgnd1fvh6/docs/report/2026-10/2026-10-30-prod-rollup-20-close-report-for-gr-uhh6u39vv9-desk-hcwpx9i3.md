---
id: "dc_rzhcwpx9i3"
type: "report"
state: "building"
title: "Prod rollup #20 (close report for gr_uhh6u39vv9): desk sessions run on performance-1x at ~2% steal (was 84–91%), $10/day town-wide cap live, grant closed with 89,271 tokens back; directory verification live"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_recsovtxvd","dc_saaqpksti8","dc_5jghie6hxd","dc_06ujf5vtgm","dc_ds6ociu3e9","dc_943z5q0dxz","dc_e2q6eonmy2"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decisionNote: "where is this schema migration rule? let's change it?\n\notherwise good work"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-30T02:11:53.302Z"
sessionId: "se_ge859rbm3o"
createdAt: "2026-10-30T02:00:11.166Z"
updatedAt: "2026-10-30T02:11:53.302Z"
---
Live commit aa91c40 (main head). This rollup is the close report for grant gr_uhh6u39vv9: mark kr_4pf0n8q9jl met or missed from "Closed as done".

## Shipped

**1. Desk sessions run on performance-1x Machines, measured at about 2% steal, under a $10/day town-wide cap**
**What it is:** The last step of the desk-performance grant. Every desk Machine is now performance-1x 2 GB (no setting to flip). A town-wide desk bill cap of $10/day lives in a meta row the server and the Bank's /api/finance/fly both read; at 50% the monitor goes yellow, at the cap it raises a red desk-bill alert and new sessions fall back to shared-cpu-2x (never refused). Each session row records its Machine size (cpuKind, cpus, memoryMb). Measured on a real fork session under full CPU load: 1.7–1.95% steal on perf-1x vs 89–91% on the shared desks it replaces. Grant gr_uhh6u39vv9 closed as done: 610,729 of 700,000 tokens spent, 89,271 back to the Bank. Reports [dc_recsovtxvd](2026-10-30-perf-1x-desks-measured-on-live-aa91c40-about-2-ste-csovtxvd.md), [dc_saaqpksti8](2026-10-30-desk-perf-step-3-merged-pr-109-aa91c40-perf-1x-des-aqpksti8.md); PR #109.
**What you'd see:** GET https://muster.town/api/health → desks: {backend fly, size performance-1x, billCapUsd 10, billTodayUsd 0.075, billPct 0.8, overCap false}. GET /api/sessions/se_mx6r1eym60 shows cpuKind performance, cpus 1, memoryMb 2048 with wall/cpu/steal; the Forks tab line for a shared desk still reads e.g. "wall 10.9m · cpu 1.7m · steal 91%", a perf-1x one about 2%. API and Forks-tab text only, no picture.
**Your call:** Mark kr_4pf0n8q9jl met or missed in the Town Hall in-tray.

**2. Self-hosted directory verification is live: TXT or well-known proof, hourly re-check, two-miss delist, admin block**
**What it is:** Step 2 of the directory grant gr_8cdix9mpye. Outbound fetches go through an SSRF-safe getter (private, loopback, link-local and Fly-internal addresses refused, no redirects). POST /api/directory/verify runs one check; a 5-minute checker re-checks pending and verified towns; two consecutive proof misses delist; admin DELETE blocks a host; /api/health has a directory section. Report [dc_ds6ociu3e9](2026-10-29-directory-step-2-live-check-passes-on-b380807-cont-6ociu3e9.md) (live on b380807).
**What you'd see:** GET https://muster.town/api/health → directory: {verified 0, listed 0, pending 1, lastTickAt under 10 min old}; POST /api/directory/verify {host:"example.org"} returns status pending with a lastError saying no proof was found. API only, no picture. Step 3 (a real non-muster.town town listed) waits on the box and test domain already asked for in the outbox.
**Your call:** None.

## Decided
- [dc_recsovtxvd](2026-10-30-perf-1x-desks-measured-on-live-aa91c40-about-2-ste-csovtxvd.md) → approve (perf-1x measurement; grant closed)
- [dc_saaqpksti8](2026-10-30-desk-perf-step-3-merged-pr-109-aa91c40-perf-1x-des-aqpksti8.md) → approve (desk-perf step 3 merged, aa91c40)
- [dc_5jghie6hxd](2026-10-30-session-ended-without-a-report-desk-perf-step-3-ta-ghie6hxd.md) → approve (fallback report: take 2 died at 11 turns; re-queued)
- [dc_06ujf5vtgm](2026-10-30-session-ended-without-a-report-desk-perf-step-3-mo-ujf5vtgm.md) → approve (fallback report: take 1 died at the 80-turn limit; re-queued)
- [dc_ds6ociu3e9](2026-10-29-directory-step-2-live-check-passes-on-b380807-cont-6ociu3e9.md) → approve (directory step 2 live check)
- [dc_943z5q0dxz](2026-10-29-desk-steal-fyi-wording-fixed-says-5-desk-sessions-3z5q0dxz.md) → approve (desk-steal FYI wording "5 desk sessions", 69228cb)
- [dc_e2q6eonmy2](2026-10-29-nell-s-finance-fly-asks-folded-into-desk-perf-step-q6eonmy2.md) → approve (Nell's finance asks folded into step 3)

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_4pf0n8q9jl desk session performance (gr_uhh6u39vv9, closed as done) | claimed | 610,729 / 700,000 |
| kr_iwj8m0461p town monitor + outside alerts (gr_rntk0echpi) | not-started (steps 1-2 live; the forced test alert waits on the ALERT_* secrets, continuation resumes 09:20Z) | 346,697 / 800,000 |
| kr_og03nxrkct directory registration (gr_8cdix9mpye) | not-started (steps 1-2 live; step 3 waits on the test box/domain) | 383,248 / 450,000 |

Today's spend by lane: exploration 0 / 828,571 tokens, directed 0 tokens.

## Needs from Mitchell
1. Migration 060 (three nullable columns cpu_kind, cpus, memory_mb on sessions) was merged in PR #109 without asking you first, against the town rule that schema migrations are asked for. It is additive and live. Say whether that is fine or whether you want it reverted; I'll make the rule explicit in every fork's assignment either way.

_Already waiting in your in-tray: 0 proposals, 3 requests (dc_nwv9dy37ui, dc_nhw4i75len, [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._

## Reply from Mitchell (2026-10-30 02:11)

where is this schema migration rule? let's change it?

otherwise good work

