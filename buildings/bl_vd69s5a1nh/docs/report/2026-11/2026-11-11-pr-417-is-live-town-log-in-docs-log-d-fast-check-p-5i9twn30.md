---
id: "dc_do5i9twn30"
type: "report"
state: "building"
title: "PR #417 is live (town log in docs/log.d, fast check, pre-push hook); the CI-under-3-minutes grant is at its ceiling: step 1 cut tests 25% but the 3-minute target will miss, cut or adjust"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_cz1o2hx3z5","dc_t7fehmhdwb","dc_ko8t4vglyj"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/417","https://github.com/mitchellgordon95/muster-town/pull/247","https://muster.town/api/health"]}
tags: ["rollup","folded"]
verdict: "stop"
decision: "approve"
decisionNote: "Folded into the in-tray row of gr_sczsxd9ztm: its ask shows there (1:1 mt_7b4zc7yja3)."
decidedBy: "system"
decidedAt: "2026-11-11T02:04:30.833Z"
sessionId: "se_u7r73ztotx"
createdAt: "2026-11-11T02:04:30.804Z"
updatedAt: "2026-11-11T02:04:30.833Z"
---
Live: d30c6f8 since 2026-11-10 22:01 UTC (CI deploy; our PR #417 went live as 03364d14 at 21:29Z).

## Shipped

**1. The town log no longer conflicts, `check --fast` catches what CI catches, and a pre-push hook runs it**
**What it is:** The whole plan of the PR-round-trips grant you funded yesterday, now live on main. docs/log.md is frozen at 355 lines; each new log entry is its own file in docs/log.d/, and check:docs refuses a PR that appends to the old file (116 hand-resolved conflicts in 10 days before this). `npm run check --fast` runs knip and the tests that read a changed docs or config file. A tracked `.githooks/pre-push` runs that check before every push, 30 to 60 s on a desk. PR #417, merge 03364d14; report [dc_cz1o2hx3z5](2026-11-10-pr-417-merged-as-03364d14-town-log-moves-to-docs-l-1o2hx3z5.md), FYI [dc_0g5zclwr09](../../../../town-hall/docs/fyi/2026-11/2026-11-10-town-log-entries-now-go-in-docs-log-d-not-docs-log-5zclwr09.md).
**What you'd see:** On main: docs/log.d/ with a README and 3 entries, docs/log.md unchanged. From any desk: a push prints the check line first and an unused export is refused in about 9 s. Three open PRs (#418 Prod, #416 Onboarding, #118 UI/UX) still append to docs/log.md and must move their line after they merge main; the FYI tells them how. API and CLI only, so no picture. The first-run-failure key result (under 6%, from 13%) is read after 7 days, on 11-17.
**Your call:** None. The hook-default question from my last rollup still stands: it is on for every desk unless you say opt-in.

**2. The CI-under-3-minutes grant has spent its 120,000 and is held: tests are 25% faster, but the 3-minute target will miss**
**What it is:** Step 1 (test databases start from one schema image, PR #247) is live. Step 2 measured one root vitest run instead of six sequential runs: 498 s against 507 s on a desk, about 2%, under the 10% bar, so nothing shipped ([dc_t7fehmhdwb](2026-11-10-gr-sczsxd9ztm-step-2-one-root-vitest-run-saves-2-4-fehmhdwb.md)). Step 3 read the 5 green main runs since the merge: tests median 164 s (152 to 175), total 192 s (175 to 204), against 220 s and 249 s in the 6 runs just before it ([dc_ko8t4vglyj](2026-11-11-gr-sczsxd9ztm-step-3-5-of-10-green-runs-since-247-8t4vglyj.md)). The suite had grown from 158 s on 11-06 to 220 s before the fix landed, so the key result of tests at most 110 s and total at most 140 s misses by about 50 s; five more runs at plus or minus 15 s cannot close that. Half the test step is the core package's per-file cost, which no step of this grant touches.
**What you'd see:** Actions → ci → job "check" → the `check:` line in each main run's job summary. In the Town Hall in-tray: the grant's gate with its reports and key-result evidence.
**Your call:** Cut the grant now (recommended: the first key result stays claimed, the second is missed, and the pending weekly timing watch keeps reading runs if you approve its retainer), or adjust it by about 30,000 tokens so the parked step-3 session reads the last 5 of 10 runs tonight; those numbers will not change the verdict.

## Decided
- [dc_cz1o2hx3z5](2026-11-10-pr-417-merged-as-03364d14-town-log-moves-to-docs-l-1o2hx3z5.md) → approve (PR #417 merged as 03364d14; 7-day observation scheduled for 11-17 22:00Z, then close)
- [dc_t7fehmhdwb](2026-11-10-gr-sczsxd9ztm-step-2-one-root-vitest-run-saves-2-4-fehmhdwb.md) → approve (step 2: root vitest run saves about 2%, under the 10% bar, not shipped)
- [dc_ko8t4vglyj](2026-11-11-gr-sczsxd9ztm-step-3-5-of-10-green-runs-since-247-8t4vglyj.md) → approve (step 3: 5 of 10 runs read, kr_9xqxj8v5cl claimed, kr_0xk1ex7tus at-risk; continuation held at the grant's ceiling)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_sczsxd9ztm CI check under 3 min | kr_9xqxj8v5cl PR #247 live on main | claimed (aacc9fe6 is an ancestor of live d30c6f8f, /api/health at 01:59Z) | at the 120,000 ceiling, held (step reports booked 106,524 plus two sessions not yet in a report; exact on the grant) |
| gr_sczsxd9ztm | kr_0xk1ex7tus tests ≤110 s, total ≤140 s over 10 green main runs | at-risk (5 runs: 164 s / 192 s; will miss by about 50 s) | — |
| gr_baf19xtg7p PR green on first push | kr_sbqqx7548z no merge-main commit resolves docs/log.md | on-track (log.d live; 7-day window to 11-17 21:07Z) | 20,903 booked to [dc_cz1o2hx3z5](2026-11-10-pr-417-merged-as-03364d14-town-log-moves-to-docs-l-1o2hx3z5.md) plus the first session / 300,000 |
| gr_baf19xtg7p | kr_vcv244638c check:docs refuses a new docs/log.md line | claimable (live since 21:29Z) | — |
| gr_baf19xtg7p | kr_5qrusz6ivw every file-reading test is in the fast map | claimable (live since 21:29Z) | — |
| gr_baf19xtg7p | kr_o6jibyr7jj PR first-run failure rate under 6% | not-started (read after 11-17 21:07Z) | — |
| gr_7op2v8fjcl red-main fixer | kr_mvj61meiwx main's CI state in /api/health | claimed ([dc_ypesutja1t](2026-11-05-gr-7op2v8fjcl-9f2d28f-is-live-and-api-health-main-esutja1t.md)) | ≈662,000 / 1,000,000 (11-08 read; final 11-12 07:00Z) |
| gr_7op2v8fjcl | kr_hsfxuz8tnx one named fixer per red main | on-track (no red main yet) | — |
| gr_7op2v8fjcl | kr_09nhvvwc1a 7-day no-duplicate-fix window | on-track (midpoint clean) | — |

Spend today by lane: exploration 0 tokens (15,798,066 free under the goal), directed 0 tokens.

## Needs from Mitchell
Nothing needed beyond the grant's own gate.

_Already waiting in your in-tray: 0 proposals, 0 requests, 3 rollups ([dc_fhv9gez4iy](2026-11-08-work-routing-step-1-is-live-pr-394-3320f44f-a-job-v9gez4iy.md), [dc_hpgpwetlrm](2026-11-08-work-routing-is-done-and-soaked-steps-2-3-and-the-gpwetlrm.md), [dc_56or1chb7y](2026-11-10-ci-step-1-is-live-test-dbs-start-from-one-schema-i-or1chb7y.md))._
