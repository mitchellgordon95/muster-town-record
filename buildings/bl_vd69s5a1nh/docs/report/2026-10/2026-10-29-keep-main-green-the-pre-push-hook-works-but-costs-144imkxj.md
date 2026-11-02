---
id: "dc_nj144imkxj"
type: "report"
state: "building"
title: "Keep main green: the pre-push hook works but costs 31 min per desk push; one decision on branch protection decides whether PR #71 ships"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_i0qz78d475","dc_hsjzft4ds2","dc_bp0drrs0ao","dc_jfu3h09hks"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/71","https://github.com/mitchellgordon95/muster-town/actions/runs/40791811123"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T03:47:44.890Z"
sessionId: "se_hxsh36np82"
createdAt: "2026-10-29T00:10:38.184Z"
updatedAt: "2026-10-29T03:47:44.890Z"
---
Nothing merged since the last rollup; main is at 06be2d1.

## Shipped

**1. Pre-push hook built and proven, held as a draft (PR #71)**
**What it is:** Finn's step 1 of gr_x5gnnmo7yi: a `.githooks/pre-push` that runs check:docs, check:deadcode, typecheck and tests and refuses the push on the first failure, wired in by root `prepare` and the desk workspace. Report [dc_i0qz78d475](2026-10-29-keep-main-green-step-1-pre-push-hook-works-pr-71-c-qz78d475.md). A deliberately broken test was refused and nothing reached the remote; CI run 40791811123 green on attempt 1.
**What you'd see:** Nothing in the UI; this is a repo change. On a desk the hook takes 31 min 12 s per push (typecheck alone 779 s) against about 2 min 20 s for the same steps in CI: desks are 2 vCPU / 2 GB and tsc ran at about 20% CPU. A 30-minute mandatory gate would make `--no-verify` the habit, so Finn did not merge and I agreed. No picture: nothing visible changed.
**Your call:** See Needs below (one decision).

**2. Why main goes red: untested direct pushes, not flakes**
**What it is:** Finn's root cause, reports [dc_bp0drrs0ao](2026-10-28-ci-red-on-main-is-untested-pushes-not-flakes-v12-d-0drrs0ao.md) and [dc_jfu3h09hks](2026-10-28-stale-state-drain-flake-1-s-waitfor-timeout-plus-a-u3h09hks.md). None of the last 200 main runs were retried; 4 of the last 20 were red, every one a push straight to main that nobody tested first (duplicate isManager, the manual.md word cap twice, the v12 desk_slots fixture, a duplicate migration in the #65 merge). The one true flake (stale-state drain, run 40454959781) is runtime.stop() not awaiting the redeployer's drain.
**What you'd see:** GitHub Actions on main: the red runs each have a green follow-up commit minutes later. Repo-only; no picture.
**Your call:** None. Steps 2 (v12.test.ts migrates forward instead of hand-undoing 47 migrations) and 3 (stoppable redeployer plus a regression test) are already queued to Finn and don't depend on the hook.

## Decided
- [dc_i0qz78d475](2026-10-29-keep-main-green-step-1-pre-push-hook-works-pr-71-c-qz78d475.md) → approve (PR #71 stays a draft, not merged; follow-up assigned once Needs is answered)
- [dc_hsjzft4ds2](2026-10-28-gr-x5gnnmo7yi-keep-main-green-on-attempt-1-cut-int-jzft4ds2.md) → approve (gr_x5gnnmo7yi cut into 4 chained steps)
- [dc_bp0drrs0ao](2026-10-28-ci-red-on-main-is-untested-pushes-not-flakes-v12-d-0drrs0ao.md) → approve (root cause: untested pushes)
- [dc_jfu3h09hks](2026-10-28-stale-state-drain-flake-1-s-waitfor-timeout-plus-a-u3h09hks.md) → approve (stale-state drain flake root cause)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_cm5qb2wqh7 CI on main green on attempt 1 | gr_x5gnnmo7yi | on-track (step 1 built, steps 2–3 queued) | 42,693 / 150,000 tokens at cut time; Finn's step 1 session adds to it |

Today's spend by lane: exploration 0 / 828,571 tokens, directed 0 tokens.

## Needs from Mitchell
1. Decide the gate for main, one of: **(b)** turn on branch protection for main in GitHub with the `check` job required, so every building pushes a branch and merges with `gh pr merge --auto --merge` (about 2 min of CI wait, and an untested commit can never land); this loosens the town-wide "commit straight to main" rule, so it is yours. Or **(a)** keep direct pushes and drop the hook: then kr_cm5qb2wqh7 rests on steps 2 and 3 plus a building rule, with no enforcement. Finn and I recommend (b), with PR #71's hook kept as an opt-in local tool. Reply in words and I assign the rework or the close of #71.

_Already waiting in your in-tray: 1 proposal (gr_8ve21typt6), 0 requests, 0 rollups._
