---
id: "dc_9mptbrwa86"
type: "report"
state: "building"
title: "Checkpoint gr_75eq6h3ltp (fast check): `npm run check` live on main, measured on a desk at 2m50s cold / 18s repeat, CI 1m27s; kr_939kp3vjxc claimed; 155,390 / 120,000; step 3 (PR #71 hook opt-in) still open"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vtia5kzu2c","dc_wh71cali3c","dc_tt1fskf9mq"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Mara: gr_xurio0oki5 (80k timings history doc) was rejected. Instead, one small assignment under kr_8wilbokqcn: the CI check job writes the per-step `check:` tim"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T15:41:20.668Z"
sessionId: "se_b7lmyibkug"
assignmentId: "as_gp60vpn4zf"
costUsd: 2.4143139500000004
tokens: 48286
turns: 21
createdAt: "2026-10-29T05:04:09.062Z"
updatedAt: "2026-10-29T15:41:20.668Z"
---
Live commit: main 2d4a490 (PR #74, Finn, merged 2026-10-29 04:47Z; `/api/health` shows it).

## Shipped
**1. One `npm run check` with per-step timings, under all three targets on an unthrottled desk**
**What it is:** A root `npm run check` runs docs, dead code, typecheck and tests in order, stops at the first failure and ends with one timing line; `npm run check --fast` typechecks from the incremental cache and runs only the tests affected since main. The six node packages typecheck as one tsc program and vitest gets 2 workers on a 2-vCPU desk. CI's `check` job runs the same command. PR #74 (2d4a490), Finn's reports [dc_wh71cali3c](2026-10-29-fast-check-step-1-the-31-min-was-89-hypervisor-ste-71cali3c.md) (measure) and [dc_tt1fskf9mq](2026-10-29-fast-check-step-2-npm-run-check-with-per-step-timi-1fskf9mq.md) (build); Finn's own desk runs were throttled (89–92% hypervisor steal), so I re-timed on my desk this session at 0.6% steal.
**What you'd see:** Terminal and GitHub Actions only, so no picture. On my desk, main 2d4a490, tsc cache cleared, then after touching one core test file:
```
check: docs 0s | deadcode 7s | typecheck 26s | tests 2m16s | total 2m50s        (170 s wall, 2.1 s steal)
check --fast: docs 0s | typecheck 8s | tests 10s | total 18s                     (1 test file, 5 tests)
```
Actions, main run 40819679824: check job 1m27s, green on attempt 1 (was ~2m20s). A deliberately broken test (89817ee) turned run 40818523011 red; its revert e4f089a was green.
**Your call:** None here; the continue/cut decision is under Needs.

## Decided
- [dc_vtia5kzu2c](2026-10-29-gr-75eq6h3ltp-fast-check-on-a-desk-cut-into-4-chai-ia5kzu2c.md) (Mara: grant cut into 4 chained steps) → approve.
- [dc_wh71cali3c](2026-10-29-fast-check-step-1-the-31-min-was-89-hypervisor-ste-71cali3c.md) (Finn, step 1: the 31 min was 89% steal; unthrottled desk ~4.5 min; two levers worth ~92 s) → approve.
- [dc_tt1fskf9mq](2026-10-29-fast-check-step-2-npm-run-check-with-per-step-timi-1fskf9mq.md) (Finn, step 2: `npm run check` on main, CI 1m12s, desk runs throttled) → approve; the desk-size call deferred to this rollup.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_939kp3vjxc Fast: `npm run check` < 3 min cold, < 1 min after a one-file change, CI check job < 3 min (how to check: a filed report with timed desk runs under the targets; the CI `check` job on main under 3 min in Actions) | the fast-check grant, at checkpoint | **claimed** (this report is the filed desk timing; Actions shows the CI job) | 155,390 / 120,000 |

Testing plan, what it showed:
- Cold and warm desk timings measured, not estimated: yes, the two lines above, from my desk, 0.6% steal; Finn's throttled runs (21m39s cold, 8m09s fast) are in [dc_tt1fskf9mq](2026-10-29-fast-check-step-2-npm-run-check-with-per-step-timi-1fskf9mq.md) with their steal numbers.
- CI still runs the full check set: yes, the check job runs docs, deadcode, typecheck, tests; the broken test made run 40818523011 red.
- The repeat run only typechecks and tests what changed: yes, typecheck 8 s from the tsbuildinfo cache against 26 s cold, vitest ran 1 of 73 files.

Caveats: the cold margin is 10 s, and the target holds only when the desk gets its CPU; a throttled desk turns the same work into ~22 min. The grant's stop condition has one open item: step 3, PR #71's pre-push hook reworked as an opt-in (`npm run hooks:install`) and merged, or #71 closed; #71 is still an open draft. Why over budget: the cut session (46,713) plus Finn's two steps (47,259 and 61,418) each ran a full measurement; step 3 and my close-out (held assignments as_jf7kxyetsb and as_ysuviv0567) were never reached.

Today's spend by lane: exploration 0 / 828,571 tokens; directed 73,023 tokens.

## Needs from Mitchell
1. Continue this grant with about 30,000 more tokens for step 3 (the hook as an opt-in on top of the 18 s fast path, then close), or cut it now: then I close PR #71 unmerged and the key result stands on today's numbers. My recommendation: continue; "local feedback before pushing" is half the grant's title and the fast path now makes the hook cheap.
2. Desk CPU: shared vCPUs lose 89–92% of their time to the hypervisor under sustained load (Finn's measurement), which is what made the hook take 31 min. Say whether desks get dedicated vCPUs, or whether "under 3 minutes on an unthrottled desk" is the standard we hold to.

_Already waiting in your in-tray: 2 proposals (gr_8ve21typt6, gr_xurio0oki5), 1 request ([dc_i98nlryg1h](../../../../../town-hall/outbox/2026-10/2026-10-29-flip-code-legibility-settings-budget-mode-to-forks-8nlryg1h.md)), 1 rollup ([dc_c2e9ekl3eq](2026-10-29-checkpoint-gr-x5gnnmo7yi-keep-main-green-v12-test-e9ekl3eq.md))._
