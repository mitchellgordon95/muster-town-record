---
id: "dc_9c7z6zdwkl"
type: "report"
state: "building"
title: "Red-main fixer (gr_7op2v8fjcl) steps 1–2 are live: a red main now gets exactly one named fixer; PR #343 narrows \"red\" to failed code checks; 13% of PR CI runs fail and docs/log.md conflicts in 116 merges (proposal gr_baf19xtg7p in your in-tray)"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_7f8oi4qhpx","dc_88z3ntb7ia","dc_xwh9p1jqvm","dc_b5xw6iuged","dc_9quo2utt6x","dc_pfe5k9ghbf","dc_x7nfxaemoc","dc_vfqwmhmai2"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/330","https://github.com/mitchellgordon95/muster-town/pull/343","https://github.com/mitchellgordon95/agent-town/actions/workflows/ci.yml"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-05T07:00:59.204Z"
sessionId: "se_sryyb3cesj"
createdAt: "2026-11-05T00:09:46.414Z"
updatedAt: "2026-11-05T07:00:59.204Z"
---
Live: aa6f4fb since 2026-11-04 20:40 UTC (3.5 h ago). It contains ed953de (PR #330, verified live by a fork at 19:18Z); 9f2d28f (PR #343, merged 19:33Z) should be in it too and a fork is confirming that now (as_5tujrhy3o8).

## Shipped

**1. A red main now gets exactly one fixer, named in every desk brief and `look`**
**What it is:** Step 2 of the red-main grant. When the runtime reads main's CI as red at a commit, it queues one fix assignment to the building of the agent who wrote that commit (falling back to this building), stores the fixer on the `mainCi` record so repeated polls and restarts never queue a second one, and every brief and `look` carries one line: "Main is red: CI failed on <sha> (<step>) since … Fixer: … Unless you are the fixer, don't push a fix." PR #330, merge ed953de. The red path is proven by tests (invariant 11) and will first run live at the next real red main; the two scheduled step-3 checks (11-08 and 11-12) watch for it.
**What you'd see:** `curl https://muster.town/api/health` → `main` is `{state, sha, failedStep, since, fixer, checkedAt}`; right now state is pending/green and `fixer: null`, so no brief shows a line. No picture: nothing is visible while main is green.
**Your call:** None.

**2. "Red" now means a failed code check only, not a cancelled run or a failed deploy job**
**What it is:** Before this fix, a `promote`/`image` job that failed or was cancelled after a green `check`, or a `check` run cancelled by the next push, would have read main as red and queued a fixer for nothing (during yesterday's merge storm this pattern occurred on three heads; the head moved before the poller caught it each time). Now main is red only when a code check failed, a cancelled check reads pending, and deploy jobs are ignored (`mainStateOf`, runtime pr-checks.ts:61, invariant 10, two new tests). PR #343, merge 9f2d28f.
**What you'd see:** API-only. A failed deploy no longer shows in `main`; it shows only as `/api/health` `commit` lagging origin/main.
**Your call:** None.

**3. Where PR round-trips are wasted: 13% of PR CI runs fail, and docs/log.md conflicts in 116 of 195 hand-resolved merges**
**What it is:** An exploration over 10 days of CI (2026-10-25 → 11-04): 59 of 442 PR runs failed; the 97 failed runs break down as knip dead code 24, check:docs 13, typecheck 10, a few failing tests 38, real breaks 9, promote-curl 503s 3. Every PR appends a line to the end of docs/log.md, so any two open PRs conflict there (PR #343 itself hit it). Each extra round-trip session costs 16k–22k tokens; the town-wide estimate is 100k–250k tokens a day, uncertain. Findings [dc_z9oix2r66w](../../note/2026-11/2026-11-05-findings-where-pr-round-trips-are-wasted-ci-failur-oix2r66w.md). The fix is proposal gr_baf19xtg7p (300k): per-change log files under docs/log.d/, `--fast` running knip plus the docs-reading tests, a tracked pre-push hook, and a 7-day check against the 13% baseline.
**What you'd see:** Nothing live yet; the proposal is in your in-tray. Note it changes AGENTS.md and root scripts for every building, and you rejected a pre-push hook once before (gr_9nvxjgajh6), so counter that part if you still don't want it.
**Your call:** None here; the proposal has its own row.

## Decided
- [dc_7f8oi4qhpx](2026-11-04-gr-7op2v8fjcl-step-1-live-api-health-main-follows-8oi4qhpx.md) → approve (step 1 live, tracks origin/main; parked for a settled green/red)
- [dc_88z3ntb7ia](2026-11-04-gr-7op2v8fjcl-step-2-a-red-main-gets-one-fixer-nam-z3ntb7ia.md) → approve (step 2 built, PR #330 parked on CI)
- [dc_xwh9p1jqvm](2026-11-04-gr-7op2v8fjcl-step-2-merged-pr-330-ed953de-redeplo-h9p1jqvm.md) → approve (PR #330 merged as ed953de)
- [dc_b5xw6iuged](2026-11-04-gr-7op2v8fjcl-step-2-is-live-ed953de-no-red-main-n-xw6iuged.md) → approve (step 2 verified live on 2adb84c)
- [dc_9quo2utt6x](2026-11-04-gr-7op2v8fjcl-red-main-edge-cases-a-failed-deploy-uo2utt6x.md) → approve (edge cases fixed in PR #343)
- [dc_pfe5k9ghbf](2026-11-04-gr-7op2v8fjcl-edge-case-fix-merged-pr-343-9f2d28f-e5k9ghbf.md) → approve (PR #343 merged as 9f2d28f; CI promotes it)
- [dc_x7nfxaemoc](2026-11-04-gr-7op2v8fjcl-step-1-api-health-main-tracked-every-nfxaemoc.md) → approve (every main head tracked 19:30–19:49Z; no run finished, green/red still unseen live)
- [dc_vfqwmhmai2](2026-11-05-explore-13-of-pr-ci-runs-fail-and-docs-log-md-conf-qwmhmai2.md) → approve (PR round-trip findings; proposal gr_baf19xtg7p filed)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_7op2v8fjcl (funded) | kr_mvj61meiwx /api/health main state | on-track (live, sha tracks every head; green/red not yet observed live) | ~448,000 / 500,000 (sum of report tokens; grant card is exact) |
| gr_7op2v8fjcl | kr_hsfxuz8tnx one fix assignment per red sha, fixer in briefs | on-track (live in ed953de + 9f2d28f; red path CI-proven, not yet seen live) | |
| gr_7op2v8fjcl | kr_09nhvvwc1a no duplicated fixes over 7 days | not-started (sc_zteqlaunbx 11-08, sc_ylx02vdi8z 11-12) | |

Spend today by lane: exploration 40,880 tokens; directed 171 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_baf19xtg7p), 2 requests ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md), [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md)), 1 rollup ([dc_2udlyqwgev](2026-11-04-gr-a5ct690l7a-one-agent-model-closed-as-done-spend-dlyqwgev.md))._
