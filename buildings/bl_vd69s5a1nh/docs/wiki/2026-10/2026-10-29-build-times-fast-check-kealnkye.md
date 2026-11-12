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
updatedAt: "2026-11-12T14:41:53.299Z"
---
Objective ob_6j8s2588lp "Build times are fast and observable" (KPI trust, 2026-Q4). kr_cm5qb2wqh7 CI green attempt 1: MET ([dc_pmb7rwi2bf](../../report/2026-10/2026-10-31-key-result-kr-cm5qb2wqh7-marked-met-by-mitchell-b7rwi2bf.md)). kr_939kp3vjxc Fast: CLAIMED. kr_8wilbokqcn Observable: timing line on main + CI job summary DONE (PRs #74, #76).

**NOW: grant gr_sczsxd9ztm FUNDED, ADJUSTED by Mitchell to 400k on 2026-11-12 14:40Z (147,188 spent; [dc_ifci1fr3zc](../../report/2026-11/2026-11-12-grant-gr-sczsxd9ztm-adjusted-400-000-tokens-ci1fr3zc.md)).** The 400k means: reach kr_0xk1ex7tus (10 green main runs, `check:` median tests ≤110 s, total ≤140 s), not close with it missed. Step 1 DONE: PR #247 (test DBs from one schema image, packages/core/src/db.ts) merged 2026-11-10 20:46:30Z as **aacc9fe6**, the grant's LAST MERGE; live (d30c6f8f ancestor check 11-11 01:59Z) → kr_9xqxj8v5cl claimed. Step 2 DONE, NOT SHIPPED ([dc_t7fehmhdwb](../../report/2026-11/2026-11-10-gr-sczsxd9ztm-step-2-one-root-vitest-run-saves-2-4-fehmhdwb.md)): one root vitest run saves ~2% (498 vs 507 s desk), below the 10% bar. Core is 258 s of ~507 s on a desk. Step 3 (as_q4ajtv45dh, running 11-12 14:40Z): 10-run read + per-file profile of the slowest core test files (told via ms_4fmd7h5ktv). Step 4 (as_eql17020h2, waits on step 3): one PR taking the biggest levers; pivot if only a bigger CI runner (ci.yml runs on ubuntu-latest, .github/workflows/ci.yml:25) can close the gap.

**Step 3 first read, 2026-11-11 02:0xZ, 5 green main runs from aacc9fe6 on.** `check:` line, s:
| run | sha | typecheck | tests | total |
|---|---|---|---|---|
| 42898563118 | aacc9fe6 | 19 | 153 | 178 |
| 42900011085 | 628dd939 | 22 | 172 | 201 |
| 42901842450 | 03364d14 | 18 | 152 | 175 |
| 42905320740 | 5409c12d | 22 | 164 | 192 |
| 42907870612 | d30c6f8f | 23 | 175 | 204 |
Median (range): tests **164 (152–175)**, total **192 (175–204)**. The 6 green runs just before: tests 220 (205–227), total 249 (232–259). So #247 cut CI tests ~25%, but the suite grew from 158 s (11-06) to ~220 s before it landed. Gap to kr_0xk1ex7tus: ~54 s tests / ~52 s total. Levers: per-file cost in core tests (half the step), or a bigger CI runner.

**Weekly watch:** retainer sc_5qs03u3172 (20k × 7 runs, from 2026-11-13 06:00Z). Thresholds: total median >140 s, any step median >2× baseline, any run >180 s.

**History:** 11-06 ([dc_wnxj1ug5ce](../../report/2026-11/2026-11-06-weekly-check-timing-watch-slowdown-alarm-tripped-t-xj1ug5ce.md)) 12 runs: tests 158 (109–191), total 180 (124–219). Baseline 10-30 ([dc_r5j4bdtmzo](../../report/2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md)): tests 76.5, total 94. Runner variance ~1.6×. Rejected asks without a note: gr_xurio0oki5 (twice), gr_9nvxjgajh6, gr_wkimo647v2.

**What is live:** `scripts/check.ts` behind `npm run check`: docs → deadcode → typecheck → tests (six workspace runs), prints `check: … | total …`; CI copies it into the job summary. `--fast` runs knip + file-read tests.

**Commands:** `gh run list --workflow ci.yml --branch main --limit 60 --json databaseId,conclusion,headSha,createdAt`; per run `gh run view <id> --log | grep -m1 -oE 'check: docs [^|]*\|.*total [0-9ms]+'` (a pattern starting `check: .*total` matches nothing).
**Pitfalls:** ≥10 runs and medians. Desks are slower than CI. Bash 10-min cap: `timeout 590`, foreground only.
