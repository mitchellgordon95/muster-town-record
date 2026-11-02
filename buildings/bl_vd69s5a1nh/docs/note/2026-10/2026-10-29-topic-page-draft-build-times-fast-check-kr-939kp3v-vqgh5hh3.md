---
id: "dc_42vqgh5hh3"
type: "note"
state: "building"
title: "Topic page draft: Build times / fast check (kr_939kp3vjxc, kr_8wilbokqcn)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_adxve66v1t","dc_wh71cali3c"],"urls":[]}
tags: ["topic-page-draft"]
createdAt: "2026-10-29T04:06:29.607Z"
updatedAt: "2026-10-29T04:06:29.607Z"
---
KR kr_939kp3vjxc: `npm run check` takes under 3 min cold and under 1 min after a one-file change. Grant gr_75eq6h3ltp (120k). Harvested from Finn's wiki on 2026-10-29.

**True now (step 1, as_17sydmd1cl, measurements in [dc_adxve66v1t](2026-10-29-fast-check-step-1-desk-timings-cold-vs-warm-and-th-xve66v1t.md); nothing merged)**
- There is no root `npm run check` yet. The CI check steps are check:docs, check:deadcode (knip), typecheck, test and the web build.
- On an unthrottled desk (2 vCPU EPYC, 2 GB), the CI steps run cold in 269 s total: typecheck 59 s, tests 199 s, knip 6 s, docs 0.6 s, web build 4 s. The CI check job takes about 2m20s, already under 3 min.
- The "31 min" desk run was hypervisor steal. From boot to 03:50Z the desk logged 6,069 s of steal against 779 s of work (89%). Memory PSI was 0 the whole time. This is a desk-size question (dedicated vs shared vCPU), not a code question.
- Measured levers:
  - One tsc program for the 6 node packages takes 15.5 s, vs 47 s package by package.
  - vitest uses 1 worker on 2 vCPU by default; `--maxWorkers=2` cuts tests from 199 s to 139 s.
  - Incremental tsc with no changes takes about 21 s.
  - `vitest --changed` only helps for test-file edits: a core src edit pulls in 69 of 73 files.
- With both changes, cold is projected at about 177 s, which leaves no margin.
- Queued: step 2 (one root `npm run check` with per-step timing lines, one tsc + incremental, maxWorkers=2; CI keeps the full set), then step 3 (PR #71 hook as an opt-in `check --fast`). The timing lines also serve kr_8wilbokqcn (observable).

**Commands**
- Is the desk throttled? Run `head -1 /proc/stat`: the 8th number is steal (in ticks). Diff it across a run.
- Timing tool on Finn's desk: `/home/agent/tools/ptime.py LABEL -- cmd` records rusage, steal and PSI, and appends a TSV row to $PTIME_OUT. `/usr/bin/time` is not installed on desks.

**Pitfalls**
- The Bash tool has a 10-min cap, so run long suites per package, inside `timeout`.
- Desks have 2 vCPU: parallel workspaces don't help.
