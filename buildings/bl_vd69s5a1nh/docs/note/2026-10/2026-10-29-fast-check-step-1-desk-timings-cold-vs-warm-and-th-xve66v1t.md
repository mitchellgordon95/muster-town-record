---
id: "dc_adxve66v1t"
type: "note"
state: "building"
title: "Fast check step 1: desk timings, cold vs warm, and the CPU diagnosis (kr_939kp3vjxc)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["fast-check","gr_75eq6h3ltp","timings"]
createdAt: "2026-10-29T04:05:03.959Z"
updatedAt: "2026-10-29T04:05:03.959Z"
---
Measured 2026-10-29 03:50–04:04Z on Finn's desk, main 2d8694d. Assignment as_17sydmd1cl, grant gr_75eq6h3ltp. These are measured numbers, not estimates, except where a row says "sum". `/usr/bin/time` isn't installed on desks, so every row comes from a wrapper (/home/agent/tools/ptime.py). It calls os.wait4 to get rusage (user, sys, max RSS) and diffs /proc/stat (steal) and /proc/pressure (PSI) around each command. Raw rows: /home/agent/fastcheck/{cold,warm}.tsv on Finn's desk.

## Desk
2 vCPU AMD EPYC, 1968 MB RAM, no swap. Before the run: load 0.07, PSI cpu some avg60 0.23%, memory 0. After the run: load 1.67, cpu some avg60 14%. **Memory PSI total = 0 since boot**, so the desk never stalled on memory.

## 1. Cold run, step by step (s = seconds, wall clock)
| step | wall s | user s | sys s | CPU % (of 1 core) | max RSS MB | steal % |
|---|---|---|---|---|---|---|
| check:docs | 0.6 | 0.6 | 0.1 | 116 | 89 | 3 |
| check:deadcode (knip) | 6.0 | 8.2 | 0.4 | 142 | 323 | 2 |
| typecheck schema | 4.7 | 7.0 | 0.2 | 156 | 337 | 1 |
| typecheck core | 9.3 | 14.5 | 0.4 | 160 | 434 | 2 |
| typecheck runtime | 10.1 | 15.7 | 0.4 | 159 | 471 | 2 |
| typecheck server | 12.2 | 18.8 | 0.6 | 159 | 585 | 2 |
| typecheck cli | 5.1 | 8.0 | 0.3 | 161 | 328 | 1 |
| typecheck desk | 5.6 | 8.6 | 0.3 | 160 | 411 | 1 |
| typecheck web | 12.3 | 18.0 | 0.4 | 149 | 472 | 1 |
| **typecheck total (sum)** | **59.3** | 90.6 | 2.6 | | | |
| test core (73 files, 433 tests) | 87.3 | 94.7 | 8.5 | 118 | 164 | 1 |
| test runtime (22 files) | 39.9 | 33.3 | 2.7 | 90 | 173 | 1 |
| test server (24 files) | 44.1 | 50.4 | 3.5 | 122 | 183 | 1 |
| test cli | 11.3 | 14.0 | 1.4 | 137 | 134 | 1 |
| test desk | 3.0 | 3.1 | 0.5 | 118 | 140 | 1 |
| test web (29 files) | 13.8 | 11.4 | 1.5 | 93 | 163 | 1 |
| **test total (sum)** | **199.4** | 206.9 | 18.1 | | | |
| build web | 4.0 | 5.2 | 0.3 | 137 | 343 | 2 |
| **everything, cold (sum)** | **269.3 (4 min 29 s)** | | | | | |
All 586+ tests passed. The CI `check` steps, in order, as one script: about 4.5 min on this desk today, against 31 min 12 s for the hook run in [dc_i0qz78d475](../../report/2026-10/2026-10-29-keep-main-green-step-1-pre-push-hook-works-pr-71-c-qz78d475.md).

## 2. CPU or work? Throttling (hypervisor steal), not work and not memory
- The `steal` column of /proc/stat counts the time the hypervisor gave our vCPUs to someone else. **From boot (~23:19Z) to the start of this session (03:50Z): 779 s of CPU work against 6,069 s of steal.** That is 89% of the non-idle time. The desk delivered ~11% of the CPU the work asked for, so ~4 min of CPU work took ~31 min of wall clock. This window includes the 31-min hook run and the 13 min 49 s core suite of the 2026-10-29 sessions.
- **This session: 1,030 s of CPU work against 20 s of steal (2%).** Each step ran at 118–160% of one core, and tsc used ~1.55 cores (GC and parser threads), not 0.5.
- Inference (not verified): this looks like Fly's shared-vCPU quota: a burst balance runs out under sustained load, and after that the vCPU is capped. I don't know what refills the balance, or whether a ~5 min check run can trigger the cap by itself. It didn't today: 14 min of continuous load, 2% steal.
- So the 31 minutes were ~85% throttling and ~15% work. On a desk that isn't throttled, the work itself takes ~4.5 min cold.

## 3. Warm and repeat experiments (measured)
| experiment | wall s | vs cold |
|---|---|---|
| `tsc --incremental --tsBuildInfoFile /tmp/<ws>`, 1st run (all 7 workspaces, sum) | 59.9 | same as cold |
| same, 2nd run with nothing changed (sum) | 20.9 | −39 s |
| same, after appending one export to core/src/names.ts (sum of 7) | 42.0 | −17 s (core, runtime, server re-check fully: 9.8 / 9.5 / 11.8) |
| same, after a one-line change to web/src/api.ts (web only) | 13.6 | none (api.ts is imported everywhere in web) |
| **one tsc program for schema+core+runtime+server+cli+desk** (temp root tsconfig, same options) | **15.5** | vs 47.0 run separately: −31.5 s (core is re-checked inside runtime, server and cli today) |
| `vitest run --changed origin/main`, core, one test file touched | 5.8 | vs 87.3 |
| same, one src file touched (core/src/lanes.ts) | 85.3 | none: 69 of 73 files depend on it |
| same, nothing changed | 0.8 | |
| **vitest `--maxWorkers=2 --minWorkers=2`**: core / runtime / server / cli / web | **59.0 / 24.3 / 32.2 / 11.4 / 9.4** | vs 87.3 / 39.9 / 44.1 / 11.3 / 13.8: −60 s in total |
Why the vitest flag helps: by default vitest uses cpus−1 = **1 worker** on a 2-vCPU desk, so the test files run one after another. That explains the 38% idle during test:core. With 2 workers, core runs at 185% CPU and 4% idle.

knip (6 s cold, 53 s in [dc_i0qz78d475](../../report/2026-10/2026-10-29-keep-main-green-step-1-pre-push-hook-works-pr-71-c-qz78d475.md) under throttling) looks at the whole project's files and dependencies. It only needs to run again when imports, exports or package.json change, and at 6 s it doesn't matter.

## 4. CI comparison (`check` job, last 5 main runs, 5460f80..2d8694d)
npm ci 6–9 s, check:docs 0–1 s, check:deadcode 3–5 s, typecheck 24–36 s, test 58–83 s, web build 2–3 s. The job takes ~2 min 20 s in total, **already under the 3-min CI target**. The CI runner does the same typecheck work in ~35 s against the desk's 59 s, and the tests in ~80 s against 199 s (GitHub runners have 4 vCPU, so vitest uses 3 workers).

## 5. What step 2 should do, measured savings
1. **One root `npm run check` that runs tsc once for the 6 node packages plus web** (a root tsconfig with project references, or one program as in the probe): typecheck goes from 59.3 s to ~27.8 s (15.5 measured + web 12.3 measured). Adding `incremental` with the tsbuildinfo in node_modules/.cache: ~4–14 s on a repeat run.
2. **vitest `maxWorkers: 2`** (or `poolOptions` sized to the number of CPUs): tests go from 199.4 s to ~139 s, the sum of the measured runs including desk's 3.0 s. A single root vitest `projects` run would also overlap the start-up of each workspace (not measured).
3. Print a per-step timing line, which kr_8wilbokqcn needs anyway.
- **Cold, with 1+2 (sum of measured parts): 0.6 + 6.0 + 27.8 + 139 + 4.0 ≈ 177 s ≈ 2 min 57 s.** That just meets the 3-min target on an unthrottled desk, with no margin. Tests are 78% of it, and core alone is 59 s. The next lever is core's collect time (15.8 s of the 86 s). Any cut to the files that every test imports helps every test file.
- **After a one-file change:** typecheck is ~4–14 s with incremental. A changed test file plus `vitest --changed` takes ~6 s, so **under 1 min holds**. A changed core src file still re-runs ~69 of the 73 core files (~59 s with 2 workers), which is at the 1-min line. Hitting it for src changes needs core's collect cost cut, or a related-only mode limited to direct importers.
- **Does the desk alone cap us above 3 min?** Not when it isn't throttled: 2 vCPU gives ~2 min 57 s cold with the changes above. When it is throttled (89% steal, as earlier tonight), nothing in the code gets it under 3 min: the same ~4 min of CPU becomes ~30 min. Mitchell's desk-size call is really "**dedicated vCPU or not**", not more cores. A shared vCPU that keeps its quota is fine. One that runs out turns any check into 10× wall time.

Not measured: a full end-to-end `npm run check` in one invocation (none exists yet), and how often desks run out of their quota.
