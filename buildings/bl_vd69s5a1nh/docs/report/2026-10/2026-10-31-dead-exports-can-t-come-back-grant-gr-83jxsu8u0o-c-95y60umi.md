---
id: "dc_a995y60umi"
type: "report"
state: "building"
title: "Dead exports can't come back: grant gr_83jxsu8u0o closed as done (PR #201 live in 00bf7ff), check:deadcode now fails on any unused export or type, 213 removed"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_jzzl3zsy7p"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/201"]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T22:39:17.795Z"
sessionId: "se_szvpvtjnw0"
createdAt: "2026-10-31T21:44:07.060Z"
updatedAt: "2026-10-31T22:39:17.795Z"
---
Live: 00bf7ff since 2026-10-31 21:41Z (contains c457d92, PR #201). This is the close report for grant gr_83jxsu8u0o.

## Shipped

**1. The dead-code check now covers exports and types, and 213 dead exports are gone**
**What it is:** `npm run check:deadcode` (run in every CI check job) now includes knip's exports and types checks, so a PR that leaves an exported function or type unused fails CI naming it. The 145 unused exports and 68 unused types that had piled up were removed in the same PR, along with three dead bodies they hid: the web `Feed` panel and its CSS, `placeAt`, and a `Town` re-export. PR #201 → c457d92 (Mara 1, report [dc_jzzl3zsy7p](2026-10-31-dead-exports-can-t-come-back-pr-201-merged-main-c4-zl3zsy7p.md)). API-only change: nothing in the UI changes.
**What you'd see:** On main, `npm run check:deadcode` prints no "Unused exports" or "Unused exported types" section and exits 0; the CI check job on a10095d, c457d92 and 00bf7ff is green. Adding `export function unusedProbe() {}` to any src file makes it exit 1 with `Unused exports (1) unusedProbe function packages/core/src/time.ts:70:17`. CI timing line before vs after the PR: `deadcode 5s | typecheck 19s | tests 1m55s | total 2m19s` vs `deadcode 5s | typecheck 20s | tests 1m53s | total 2m18s`.
**Your call:** None. One thing to know: main's last three runs show "failure" in the promote job only, because its redeploy curl got HTTP 503 while the lag alert was red; the check job passed each time. Separately, the CI check total (2m18s) sits above the 73–116 s baseline because the tests step grew over the last day, unrelated to this PR; the weekly timing watch will report on it on 6 Nov.

## Decided
- [dc_jzzl3zsy7p](2026-10-31-dead-exports-can-t-come-back-pr-201-merged-main-c4-zl3zsy7p.md) → approve (work done; grant closed from this session).

## Key results

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_83jxsu8u0o (closed as done) | kr_ealc55cjf5 check:deadcode includes exports+types, 0 unused on main | claimed | 77,238 / 200,000 (122,762 returned) |
| gr_83jxsu8u0o | kr_518c748b49 covers exports and types and is green | claimed | (same) |
| gr_83jxsu8u0o | kr_7910fec063 catches a new dead export | claimed | (same) |
| gr_83jxsu8u0o | kr_31c6f67b59 no behaviour change | claimed (typecheck+tests green; the CI total is above the 73–116 s baseline for reasons predating the PR, see above) | (same) |
| gr_gh3lnuihw9 (funded) | kr_4jhab4c5cn no high/critical advisory in prod deps, audit workflow | not-started (step 1 queued as as_cvgu0h7kp0) | 0 / 500,000 |
| gr_gh3lnuihw9 | kr_46398efa33, kr_6805523069, kr_0800718a7a, kr_5a90181c60 | not-started | 0 / 500,000 |

Today's spend by lane: exploration 150,281 tokens (free under the goal: 0), directed 177,581 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 1 request (dc_bn4s4m7cq3), 0 rollups._
