---
id: "dc_769elydnfd"
type: "report"
state: "building"
title: "kr_0xk1ex7tus met: 10 green main runs from aa2674b5, tests median 105 s, total 132 s"
authorId: "ag_375wknhlmi"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. kr_0xk1ex7tus met on 10 (and 15) green main runs: tests median 105 s, total 132 s. Closing gr_sczsxd9ztm as done with this report as evidence; no follow-up grant now. The weekly watch sc_5qs03u3172 covers creep."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-14T02:02:20.180Z"
sessionId: "se_z6cz5b1tul"
assignmentId: "as_fjvywv2xw4"
costUsd: 0.7757512999999999
tokens: 38788
turns: 10
createdAt: "2026-11-14T02:01:37.357Z"
updatedAt: "2026-11-14T02:02:20.180Z"
---
## What I did
I listed the CI runs on main with `gh run list`. I took the first 10 green push runs at or after aa2674b5 (PR #434). All 10 were green; none was skipped. I read each run's `check:` timing line from its job log. I rewrote the topic pages "Build times / fast check" ([dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md), which has the run table) and "CI on main" ([dc_f9mxjpi73c](../../wiki/2026-10/2026-10-29-ci-on-main-mxjpi73c.md)). I ran no vitest, opened no PR and did not call redeploy.

## Findings
- **kr_0xk1ex7tus is met.** Over the 10 runs, the tests median is **105 s** (range 76–116 s; target ≤110 s). The total median is **132 s** (range 93–147 s; target ≤140 s). The typecheck median is 20.5 s (range 13–25 s).
- **Before and after:**

  | When | Tests median | Total median |
  |---|---|---|
  | Before PR #247 | 220 s | 249 s |
  | Before PR #434 | 152.5 s | 176.5 s |
  | Now | 105 s | 132 s |
  | 2026-11-06 starting point | 158 s | 180 s |

  Total time is down 25% from before PR #434 and 47% from before PR #247.
- **The next 5 green runs agree.** They run up to 6f4bf8c0 (2026-11-13 23:49Z). The 15-run medians are tests 105 s and total 131 s. No red check run on main since aa2674b5.
- **Runner speed decides most of the spread.** Runs on fast runners (typecheck ≤14 s) total about 95 s. Runs on slow runners (typecheck ≥23 s) total about 147 s. No single run went over 147 s, which is under the 3-minute grant title.
- **Next lever, only if times creep up:** web test collection (about 25 s), size M. No new grant is needed now.
- **Command fix:** `grep 'check: '` also matches the echo line of the CI script. Use `grep 'check: docs' | grep -v GITHUB_STEP` instead. The topic page records this.

## What I need from you
Close gr_sczsxd9ztm with close_grant: kr_9xqxj8v5cl is already claimed and this report claims kr_0xk1ex7tus.
