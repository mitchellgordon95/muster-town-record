---
id: "dc_drcszutzkn"
type: "report"
state: "building"
title: "Exploration: tests slowed 33% because every test DB re-runs 76 migrations; draft PR #247 cuts ~19%, proposed gr_wkimo647v2 (80k)"
authorId: "ag_vvix6m1gm3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_o3whsqb8ms","dc_r5j4bdtmzo","dc_87kealnkye"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/247"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Verified in the snapshot: openDb (core/src/db.ts:13-21) runs migrate() on every open, and main now carries 77 migration files (078_root_captain landed with #241 after you measured). The proposal gr_wkimo647v2 reaches Mitchell on its own; PR #247 stays a draft until he decides. Nothing else to do here."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-01T02:19:13.820Z"
sessionId: "se_evd8wtcyyg"
assignmentId: "as_nrwwyw9vk1"
costUsd: 1.3480537999999995
tokens: 67403
turns: 29
createdAt: "2026-11-01T02:18:57.154Z"
updatedAt: "2026-11-01T02:19:13.820Z"
---
## What I did
Pulled the `check:` timing line from 12 green main CI runs, profiled the test suites on my desk, prototyped a fix as draft PR #247 (https://github.com/mitchellgordon95/muster-town/pull/247), wrote findings [dc_o3whsqb8ms](../../note/2026-11/2026-11-01-findings-ci-tests-are-33-slower-than-the-10-30-bas-whsqb8ms.md), rewrote the topic page "Build times / fast check" ([dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md)), and proposed gr_wkimo647v2 (80k tokens) under ob_6j8s2588lp.

## Findings
- **CI got slower.** I looked at 12 green main runs (41247500767 … 41262429556). The tests step has a median of 101.5 s (range 76–129 s) and the check total 120 s (90–153 s). The 10-30 baseline was 76.5 s and 94 s, so that's +33% and +28%. It's still under the weekly watch's 140 s alarm line.
- **Cause:** `openDb` runs all 76 migrations for every new database, about 51 ms each on a desk. Core's suite opens 521 of them, which adds up to 65.5 s, or 46% of core's test time. The cost grows with every migration × every test, so the suite gets slower even when nobody touches the tests.
- **Fix in PR #247:** a new database (`:memory:` or a file that doesn't exist yet) now starts from one serialized copy of the fully migrated schema, built once per process. A copy takes 0.47 ms. The new test `core/test/db-schema-image.test.ts` checks that the copy has exactly the schema and version list you get from running every migration. On my desk, same code with and without the change: core 116.7 → 92.5 s, runtime 39.2 → 32.6 s, server 55.0 → 46.7 s, which is −19% across the three. All tests pass, and the full `npm run check` passes on the branch. Opening an existing production database works the same as before.
- **The proposal** (KRs due 2026-11-04 to 11-08): merge #247; get the median tests time back to ≤ 85 s over 10 main runs; then measure the next biggest cost, vitest's collect time (core 50 s, server 31 s). If it's worth it, run all tests as one root vitest run; if not, write down the numbers. It stops early if that second step saves less than 10%. #247 changes shared core (`db.ts`, `openDb` only).
- Unrelated: one server test failed once on a run without the change and passed on the rerun with it. I didn't investigate it.

## What I need from you
Decide on gr_wkimo647v2 in the Town Hall in-tray. Until then PR #247 stays a draft.
