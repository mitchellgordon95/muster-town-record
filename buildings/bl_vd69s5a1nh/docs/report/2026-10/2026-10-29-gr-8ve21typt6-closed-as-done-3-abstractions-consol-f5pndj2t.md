---
id: "dc_mqf5pndj2t"
type: "report"
state: "building"
title: "gr_8ve21typt6 closed as done: 3 abstractions consolidated (d30bfdd, 267c2ed, 03beade); drain flake fixed at the root; doc-drift check evidenced. Your call: mark kr_doa59kdway and kr_oubxzkl4n6 met"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_xju2gul82r","dc_gq34e2h7ys","dc_kjbyprb38d","dc_rgzsr3yt21","dc_i7crbbfpsv","dc_mkbu9vsx2h","dc_elnejxigu2"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/82","https://github.com/mitchellgordon95/muster-town/pull/85","https://github.com/mitchellgordon95/muster-town/pull/86","https://github.com/mitchellgordon95/muster-town/pull/88","https://github.com/mitchellgordon95/muster-town/pull/89"]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T23:43:32.967Z"
sessionId: "se_fiap5j7ssr"
createdAt: "2026-10-29T21:16:20.470Z"
updatedAt: "2026-10-29T23:43:32.967Z"
---
Live commit should be 03beade (redeploy called after each merge; desk image rebuilt at d30bfdd).

## Shipped

**1. Three repeated code patterns consolidated into core (grant gr_8ve21typt6 closed as done)**
**What it is:** The three abstraction-sweep candidates from Finn's sweep ([dc_0q4mlk2wuh](../../note/2026-10/2026-10-28-abstraction-sweep-1-candidates-4mlk2wuh.md)) now live in one place each. The desk's hand-copied contract types come from @muster-town/schema (PR #82 → d30bfdd, with a drift fix: the schema now carries `interrupts[].now`, which the server was already sending). A `whereOf()` helper in core/src/table.ts replaces 7 hand-rolled SQL WHERE builders (PR #88 → 267c2ed). `requireAdmin()`/`isUserAdmin()` in core/src/permissions.ts replace 10 server-side admin checks (PR #89 → 03beade). Bank code untouched. Reports [dc_kjbyprb38d](2026-10-29-gr-8ve21typt6-cut-into-3-steps-step-1-desk-contrac-byprb38d.md), [dc_mkbu9vsx2h](2026-10-29-gr-8ve21typt6-step-2-landed-whereof-replaces-the-7-bu9vsx2h.md), [dc_elnejxigu2](2026-10-29-gr-8ve21typt6-step-3-landed-requireadmin-isuseradm-nejxigu2.md).
**What you'd see:** Code-only change, no UI. On main: `git log --oneline | grep gr_8ve21typt6` shows the three commits; `grep -rn "where.push" packages/core/src` and `grep -rn 'isAdmin({ kind: "user"' packages/server/src` are empty; packages/desk/src/contract.ts is gone. Each PR and its main run passed on attempt 1. Spent 176,158 of 260,000 tokens; 83,842 returned to the Bank.
**Your call:** Mark kr_doa59kdway (abstraction sweeps) met.

**2. The stale-state drain flake is fixed at the root, not retried**
**What it is:** `runtime.stop()` now awaits the redeployer, so a drain can no longer race a stopping runtime. Regression test added and cited as invariant 9 in docs/invariants/runtime-wakes.md (Mara 1, PR #85 → f904590, report [dc_rgzsr3yt21](2026-10-29-stale-state-drain-flake-fixed-at-the-root-runtime-zsr3yt21.md)). Finn's earlier change prints a per-step timing line in the GitHub Actions job summary (PR #76 → a292c1a, [dc_gq34e2h7ys](2026-10-29-ci-check-job-writes-the-per-step-timing-line-to-th-34e2h7ys.md)).
**What you'd see:** No UI change. GitHub Actions on main: every run since f904590 green on attempt 1 (kr_cm5qb2wqh7 stays on-track); each run's Summary tab shows the check-step timing line.
**Your call:** None.

**3. Doc-drift check proven: green on main, red when a doc path breaks**
**What it is:** The evidence kr_oubxzkl4n6 asks for. Main run 40949851903 passed with check:docs; a deliberately broken path reference in PR #86 turned CI red at check:docs (run 40950031071), then the PR was closed and the branch deleted (Mara 1, [dc_i7crbbfpsv](2026-10-29-doc-drift-evidence-for-kr-oubxzkl4n6-main-green-ru-crbbfpsv.md)).
**What you'd see:** API/CI-only, no picture. GitHub Actions: the two runs above; closed PR #86 shows the red check:docs step.
**Your call:** Mark kr_oubxzkl4n6 (doc drift) met.

## Decided
- [dc_xju2gul82r](2026-10-29-grant-gr-75eq6h3ltp-cut-u2gul82r.md) → approve (town notice: gr_75eq6h3ltp cut at checkpoint, kr_939kp3vjxc claimed; held steps cancelled)
- [dc_gq34e2h7ys](2026-10-29-ci-check-job-writes-the-per-step-timing-line-to-th-34e2h7ys.md) → approve (Finn: CI job-summary timing line, PR #76 → a292c1a; PR #71 closed)
- [dc_kjbyprb38d](2026-10-29-gr-8ve21typt6-cut-into-3-steps-step-1-desk-contrac-byprb38d.md) → approve (gr_8ve21typt6 step 1, PR #82 → d30bfdd)
- [dc_rgzsr3yt21](2026-10-29-stale-state-drain-flake-fixed-at-the-root-runtime-zsr3yt21.md) → approve (drain-flake root fix, PR #85 → f904590)
- [dc_i7crbbfpsv](2026-10-29-doc-drift-evidence-for-kr-oubxzkl4n6-main-green-ru-crbbfpsv.md) → approve (doc-drift evidence, PR #86 closed)
- [dc_mkbu9vsx2h](2026-10-29-gr-8ve21typt6-step-2-landed-whereof-replaces-the-7-bu9vsx2h.md) → approve (gr_8ve21typt6 step 2, PR #88 → 267c2ed)
- [dc_elnejxigu2](2026-10-29-gr-8ve21typt6-step-3-landed-requireadmin-isuseradm-nejxigu2.md) → approve (gr_8ve21typt6 step 3, PR #89 → 03beade); then close_grant gr_8ve21typt6

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_doa59kdway abstraction sweeps | gr_8ve21typt6 (closed as done) | claimed | 176,158 / 260,000 |

No grant is funded now. Today's spend by lane: exploration 69,465 / 828,571 tokens, directed 105,376 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 1 request (dc_bn4s4m7cq3), 0 rollups._
