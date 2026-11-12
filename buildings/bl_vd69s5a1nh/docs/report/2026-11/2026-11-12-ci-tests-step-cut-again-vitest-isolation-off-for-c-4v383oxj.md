---
id: "dc_yx4v383oxj"
type: "report"
state: "building"
title: "CI tests step cut again: vitest isolation off for core and server, one run at 110 s tests / 140 s total"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_nj6bfjumtw"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-12T16:37:55.045Z"
sessionId: "se_rk7q4kzt2f"
createdAt: "2026-11-12T16:37:55.022Z"
updatedAt: "2026-11-12T16:37:55.045Z"
---
Live: 0a682c6 since 2026-11-12 16:21 UTC; it contains our PR #434 (aa2674b5).

## Shipped
**1. The CI tests step runs core and server tests without per-file isolation**
**What it is:** Vitest now keeps one module graph per worker for the core and server packages instead of re-importing everything for each test file. Import time was 77 s of core's 84 s. Runtime tests stay isolated because two files keep module-level state. This is step 4 of 4 of the "CI check under 3 minutes" grant; the grant has spent about 238,000 of its 400,000 tokens. Report [dc_nj6bfjumtw](2026-11-12-gr-sczsxd9ztm-step-4-vitest-isolate-false-for-core-6bfjumtw.md), PR #434, commit aa2674b5.
**What you'd see:** On any PR or main run in GitHub Actions, the `check:` summary line. PR #434's own run read `typecheck 23s | tests 1m50s | total 2m20s`: tests 110 s and total 140 s, against the 10-run medians of 152.5 s and 176.5 s before it and 220 s and 249 s before step 1. Core fell 83.6 s → 27.5 s, server 36.2 s → 19.6 s. No picture: CI numbers only.
**Your call:** None. The last key result needs the median of 10 green main runs from aa2674b5 at or under 110 s and 140 s; a one-shot read on 2026-11-14 at 02:00 UTC files it, and I close the grant from that report.

## Decided
- [dc_nj6bfjumtw](2026-11-12-gr-sczsxd9ztm-step-4-vitest-isolate-false-for-core-6bfjumtw.md) → approve (step 4 shipped; the 10-run read is scheduled as sc_owiul5muej).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_sczsxd9ztm (funded, 4 of 4 steps done) | kr_9xqxj8v5cl check under 3 min once | claimed | about 238,000 / 400,000 |
| gr_sczsxd9ztm | kr_0xk1ex7tus tests ≤110 s, total ≤140 s over 10 main runs | on-track (one run at 110 s / 140 s; 10-run read due 11-14) | |
| gr_baf19xtg7p (funded) | kr_vcv244638c, kr_5qrusz6ivw | claimable (PR #417 live) | step 1 of 1 booked / 300,000 |
| gr_baf19xtg7p (funded) | kr_sbqqx7548z, kr_o6jibyr7jj | on-track, 7-day window ends 11-17 21:07Z | |

Spend today by lane: exploration 0 tokens, directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 4 rollups ([dc_fhv9gez4iy](2026-11-08-work-routing-step-1-is-live-pr-394-3320f44f-a-job-v9gez4iy.md), [dc_hpgpwetlrm](2026-11-08-work-routing-is-done-and-soaked-steps-2-3-and-the-gpwetlrm.md), [dc_56or1chb7y](2026-11-10-ci-step-1-is-live-test-dbs-start-from-one-schema-i-or1chb7y.md), [dc_iq4txxz11i](2026-11-12-red-main-fixer-grant-closed-done-no-red-main-in-7-4txxz11i.md))._
