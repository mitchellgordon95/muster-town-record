---
id: "dc_87kealnkye"
type: "wiki"
state: "building"
title: "Build times / fast check"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-10-29T04:09:08.218Z"
updatedAt: "2026-11-02T03:05:57.806Z"
---
Objective ob_6j8s2588lp "Build times are fast and observable" (KPI trust, 2026-Q4), set by Mitchell at 1:1 mt_cy04ix9cc3 ([dc_grvhp5dl9l](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-mara-notes-vhp5dl9l.md)). kr_cm5qb2wqh7 CI green attempt 1: MET (see "CI on main"). kr_939kp3vjxc Fast: CLAIMED, Mitchell marks met/missed. kr_8wilbokqcn Observable: timing line on main + CI job summary DONE (PR #74, PR #76). Status 2026-11-02 (this page's updatedAt is the stamp).

**Nothing open. Build-time work is PARKED until the weekly watch alarms.** Three build-time asks were rejected without a note: the 20-run history page (gr_xurio0oki5, 2026-10-29), the manual word cap + hook (gr_9nvxjgajh6, 10-31) and the migrated-schema image + collect lever (gr_wkimo647v2, 80k, 2026-11-02 03:04Z, report [dc_drcszutzkn](../../report/2026-11/2026-11-01-exploration-tests-slowed-33-because-every-test-db-cszutzkn.md), findings [dc_o3whsqb8ms](../../note/2026-11/2026-11-01-findings-ci-tests-are-33-slower-than-the-10-30-bas-whsqb8ms.md)). Free tokens under the goal are 0 (the building's budget is gr_a5ct690l7a); re-propose only when the watch below reports a slowdown, and then as a small single-PR ask. Draft PR #247 (branch agent/mara-1/test-db-schema-image, 1 file + 1 test, green on the branch) stays open with a "parked" comment: a new database starts from a once-per-process serialized schema image (0.47 ms vs 76 migrations × 51 ms); desk gain core 116.7→92.5 s, runtime 39.2→32.6 s, server 55.0→46.7 s (−19%). Next lever after it, unmeasured: vitest collect (core 50 s, server 31 s): one root vitest run with `projects` instead of six serial workspace runs (scripts/check.ts:46).

**Weekly watch sc_45pi8pvl9q** (exploration, every 168 h from 2026-11-06 06:00Z to 2026-12-31): pulls the `check:` line from the last ~12 green main runs, compares to the baseline, rewrites this section. Slowdown = median total >140 s, a step median >2× baseline, or a run >180 s. Last measured 2026-11-01 (main af85f2a, 12 runs 41247500767 … 41262429556): tests median 101.5 s (76–129), total 120 s (90–153): +33%/+28%, under the alarm line.

**Baseline 2026-10-30 ([dc_r5j4bdtmzo](../../report/2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md)), 12 green main runs, s median (range):** docs 0 (0–1), deadcode 3.5 (3–5), typecheck 13.5 (10–18), tests 76.5 (58–93), check total 94 (73–116), whole check job 113 (89–136).

**What is live:** `scripts/check.ts` behind `npm run check`: docs → deadcode → typecheck → tests (each workspace's vitest in turn), stops at the first failure, ends with `check: docs 1s | deadcode 3s | typecheck 11s | tests 58s | total 1m12s`. `--fast` / `CHECK_FAST=1` skips knip and runs `vitest --changed <merge-base>`. One root tsconfig, incremental tsc cache, vitest `--maxWorkers max(2, cpus−1)`. CI copies the line into the job summary.

**Commands**
- Timing lines of main runs: `gh run list --workflow ci --branch main --json databaseId,conclusion`, then per run the check job id from `gh api repos/{owner}/{repo}/actions/runs/<id>/jobs` and `gh run view <id> --log --job <jobId> | grep -oE 'check: .*total [0-9ms]+'`.
- Per-file times: the log has literal `^[[..m` escapes; replace `^[` with ESC before stripping ANSI, then parse `✓ file (N tests) Xms` and `RUN … packages/<ws>`.
- Throttled? `head -1 /proc/stat`: 8th number = steal ticks (100 Hz).

**Pitfalls**
- CI runner variance ~1.6× on identical code: compare medians over ≥10 runs. Desks are slower than CI (desk full check 4m02s on 2026-11-01).
- Bash tool 10-min cap: run the full check with `timeout 590` or in the background.
- `--fast` reruns every test when a package.json or vite config changes. CI's promote job redeploys main on green.
