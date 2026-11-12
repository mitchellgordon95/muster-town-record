---
id: "dc_56or1chb7y"
type: "report"
state: "building"
title: "CI step 1 is live: test DBs start from one schema image (aacc9fe6); PR #417 (log.d, fast check, pre-push hook) is open and merges on green"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_9yxg45qbcz","dc_85lqfic1xs","dc_km8ulyvb61","dc_oo4kc5rna4","dc_3s0flygw0p"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/247","https://github.com/mitchellgordon95/muster-town/pull/417","https://muster.town/api/health"]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decisionNote: "Rollups are retired (1:1 mt_msnjkpgwdb decision 21): what this one asked is its own ask in the decision queue; what it reported is on the job threads."
decidedBy: "system"
decidedAt: "2026-11-12T23:05:49.530Z"
sessionId: "se_3oy8h95i5u"
createdAt: "2026-11-10T21:03:01.146Z"
updatedAt: "2026-11-12T23:05:49.530Z"
---
Live: aacc9fe6 since 2026-11-10 20:59 UTC (CI deploy; it carries our PR #247).

## Shipped

**1. Test databases start from one schema image, so the CI test step is shorter**
**What it is:** Step 1 of the grant you funded 40 min ago to bring the CI check back under 3 minutes. Every test that opened a database used to replay all 106 migrations; now the first open builds the schema once and the rest copy the image. On a desk the tests step fell from 451 s to 373 s (−17%, one run each). CI's own single run showed tests 174 s and total 204 s, which is inside the 1.6× runner variance and proves nothing yet. PR #247, merge aacc9fe6; reports [dc_9yxg45qbcz](2026-11-10-pr-247-brought-up-to-date-with-main-and-re-measure-xg45qbcz.md), [dc_85lqfic1xs](2026-11-10-pr-247-merged-aacc9fe6-test-dbs-start-from-one-sch-lqfic1xs.md).
**What you'd see:** The `check:` line in any main CI run's job summary (Actions → ci → job "check"). No screen changes: CI and API only, so no picture. Step 3 reads the medians of the next 10 green main runs from 02:00 UTC tomorrow and claims the under-3-minutes key result if tests ≤110 s and total ≤140 s. Step 2 (one root vitest run instead of six sequential ones) is measuring on a fork now; it ships only if it saves another 10%.
**Your call:** None.

**2. PR #417 is open: the town log stops conflicting, `check --fast` catches what CI catches, and a pre-push hook runs it**
**What it is:** The whole plan of the PR-round-trips grant you funded 20 min ago, in one PR, waiting on CI. docs/log.md is frozen at 355 lines; new entries go one file per change into docs/log.d/, and check:docs refuses a PR that appends to the old file (116 hand-resolved conflicts on it in 10 days). `npm run check --fast` runs knip again and adds the tests that read a changed non-code file. A tracked `.githooks/pre-push` runs that check before every push: 30 to 60 s on a 2-vCPU desk; an unused export is refused in 9 s. Report [dc_3s0flygw0p](2026-11-10-pr-417-docs-log-d-check-fast-with-knip-and-file-re-0flygw0p.md).
**What you'd see:** Nothing yet: Mara 1 is parked on its CI and merges it when green. After that: `docs/log.d/` on main, and every push from a desk prints the check line first.
**Your call:** The hook is on for every desk by default (`git push --no-verify` skips it). A hook was turned down twice before (PR #71), so say if you want it opt-in instead; otherwise it merges on green as built.

## Decided
- [dc_9yxg45qbcz](2026-11-10-pr-247-brought-up-to-date-with-main-and-re-measure-xg45qbcz.md) → approve (step 1: #247 rebased on main, tests −17% on a desk; merge continuation parked on CI)
- [dc_85lqfic1xs](2026-11-10-pr-247-merged-aacc9fe6-test-dbs-start-from-one-sch-lqfic1xs.md) → approve (#247 merged as aacc9fe6, no redeploy; step 2 queued)
- [dc_km8ulyvb61](2026-11-10-session-ended-without-a-report-measure-the-one-roo-8ulyvb61.md) → redirect (step 2 fork backgrounded its timing runs and ended with nothing; redo as_ad67kfdo6o with foreground-only rules, running now)
- [dc_oo4kc5rna4](2026-11-10-gr-sczsxd9ztm-step-3-parked-0-of-10-green-main-run-4kc5rna4.md) → approve (step 3 parked: 0 of 10 green main runs since the merge; resumes 02:00 UTC 11-11)
- [dc_3s0flygw0p](2026-11-10-pr-417-docs-log-d-check-fast-with-knip-and-file-re-0flygw0p.md) → approve (PR #417 opened and parked on CI; merge continuation as_dftldqs044 waits on it)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_sczsxd9ztm CI check under 3 min | kr_9xqxj8v5cl PR #247 live on main | claimed (aacc9fe6 in /api/health `commit` since 20:59Z) | ≥86,000 / 120,000 (five sessions booked; exact on the grant) |
| gr_sczsxd9ztm | kr_0xk1ex7tus tests ≤110 s, total ≤140 s over 10 green main runs | on-track (step 3 parked till 02:00Z 11-11) | — |
| gr_baf19xtg7p PR green on first push | kr_sbqqx7548z no merge-main commit resolves docs/log.md | on-track (PR #417 open, CI running) | first session not yet booked to a report / 300,000 |
| gr_baf19xtg7p | kr_vcv244638c check:docs refuses a new docs/log.md line (test) | on-track (test in #417) | — |
| gr_baf19xtg7p | kr_5qrusz6ivw every file-reading test is in the fast map (test) | on-track (test in #417) | — |
| gr_baf19xtg7p | kr_o6jibyr7jj PR first-run failure rate under 6% | not-started (7-day window after the merge, ≈11-17 to 11-19) | — |
| gr_7op2v8fjcl red-main fixer | kr_mvj61meiwx main's CI state in /api/health | claimed ([dc_ypesutja1t](2026-11-05-gr-7op2v8fjcl-9f2d28f-is-live-and-api-health-main-esutja1t.md)) | ≈662,000 / 1,000,000 (11-08 read; final 11-12 07:00Z) |
| gr_7op2v8fjcl | kr_hsfxuz8tnx one named fixer per red main | on-track (no red main yet) | — |
| gr_7op2v8fjcl | kr_09nhvvwc1a 7-day no-duplicate-fix window | on-track (midpoint clean) | — |

Spend today by lane: exploration 0 tokens (11,327,937 free under the goal), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 2 rollups ([dc_fhv9gez4iy](2026-11-08-work-routing-step-1-is-live-pr-394-3320f44f-a-job-v9gez4iy.md), [dc_hpgpwetlrm](2026-11-08-work-routing-is-done-and-soaked-steps-2-3-and-the-gpwetlrm.md))._
