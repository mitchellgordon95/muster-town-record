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
updatedAt: "2026-11-10T20:49:15.013Z"
---
Objective ob_6j8s2588lp "Build times are fast and observable" (KPI trust, 2026-Q4). kr_cm5qb2wqh7 CI green attempt 1: MET ([dc_pmb7rwi2bf](../../report/2026-10/2026-10-31-key-result-kr-cm5qb2wqh7-marked-met-by-mitchell-b7rwi2bf.md)). kr_939kp3vjxc Fast: CLAIMED, Mitchell marks met/missed. kr_8wilbokqcn Observable: timing line on main + CI job summary DONE (PRs #74, #76).

**NOW: grant gr_sczsxd9ztm FUNDED (120k).** Step 1 DONE: PR #247 (test DBs start from one schema image instead of replaying every migration in openDb, packages/core/src/db.ts) MERGED 2026-11-10 20:46:30Z, merge commit **aacc9fe6f98c02bda3822dd20a06052d8c44bda1** (merge, not squash). Desk measure before merge ([dc_9yxg45qbcz](../../report/2026-11/2026-11-10-pr-247-brought-up-to-date-with-main-and-re-measure-xg45qbcz.md), 1 CPU, 1 run each): tests 451→373 s (−17%), core+runtime+server 384→305 s (−21%). The PR's own CI run 42897504164 (pre-merge): tests 174 s, total 204 s — one run, within ~1.6× runner variance, not evidence either way. kr_9xqxj8v5cl: live once /api/health `commit` contains aacc9fe6 (CI deploys; no redeploy).

**Step 2 (one root vitest run with `projects` vs the six sequential workspace runs at scripts/check.ts:46, ship only if ≥10%): BEING REDONE as as_ad67kfdo6o.** First attempt ([dc_km8ulyvb61](../../report/2026-11/2026-11-10-session-ended-without-a-report-measure-the-one-roo-8ulyvb61.md)) produced nothing: the fork backgrounded the timing runs and ended its turn on a Monitor. Rule: time in the foreground, one Bash call per run with `timeout 590`, three interleaved pairs, medians. If step 2 ships a PR, its merge sha becomes the grant's last merge.

**Step 3 (as_cxsxvt2yvm, [dc_oo4kc5rna4](../../report/2026-11/2026-11-10-gr-sczsxd9ztm-step-3-parked-0-of-10-green-main-run-4kc5rna4.md)): PARKED**, resumes after 02:00Z 11-11; counts 10 green main runs from the grant's last merge (aacc9fe6, or step 2's merge if it ships), then claims kr_0xk1ex7tus (tests ≤110 s, total ≤140 s, due 11-14) if met. Main cadence on 11-10: ~14 runs in 3 h, so 10 runs land within a few hours of the last merge.

History page stays rejected (gr_xurio0oki5 twice). Earlier rejected asks, all without a note: gr_xurio0oki5, gr_9nvxjgajh6, gr_wkimo647v2.

**Weekly watch:** retainer sc_5qs03u3172 (20k × 7 runs, from 2026-11-13 06:00Z, pending Mitchell's approval). Thresholds: total median >140 s, any step median >2× baseline, any run >180 s.

**Run of 2026-11-06 (as_ihd1gnzwq3, [dc_wnxj1ug5ce](../../report/2026-11/2026-11-06-weekly-check-timing-watch-slowdown-alarm-tripped-t-xj1ug5ce.md)):** last 12 green main runs, seconds, median (range): docs 0.5 (0–1), deadcode 4.5 (3–6), typecheck 16 (12–22), tests 158 (109–191), check total 180 (124–219), whole job 201 (141–243). Baseline 2026-10-30 ([dc_r5j4bdtmzo](../../report/2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md)): total 94, tests 76.5, job 113. Drivers: test cases +33% (1,278→1,705), migrations 76→96 (106 on 11-10). Runner variance ~1.6× on identical code.

**What is live:** `scripts/check.ts` behind `npm run check`: docs → deadcode → typecheck → tests, stops at first failure, prints `check: docs … | total …`. `--fast` / `CHECK_FAST=1` skips knip and runs `vitest --changed`. CI (.github/workflows/ci.yml:38-43) copies the line into the job summary.

**Commands:** `gh run list --workflow ci --branch main --status success`; per run `gh api repos/{owner}/{repo}/actions/runs/<id>/jobs` (job "check"), then `gh run view <id> --log --job <jobId> | sed 's/\x1b\[[0-9;]*[A-Za-z]//g' | grep -oE 'check: .*total [0-9hms]+'`.
**Pitfalls:** variance ~1.6×, so use ≥10 runs and medians. Desks are slower than CI. Bash tool 10-min cap: use `timeout 590`, never a background task you then wait on (the session ends with your turn).
