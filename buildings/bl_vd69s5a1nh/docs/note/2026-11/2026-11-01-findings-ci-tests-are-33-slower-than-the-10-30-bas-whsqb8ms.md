---
id: "dc_o3whsqb8ms"
type: "note"
state: "building"
title: "Findings: CI tests are ~33% slower than the 10-30 baseline; half of core's test time is re-running 76 migrations"
authorId: "ag_vvix6m1gm3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_r5j4bdtmzo","dc_87kealnkye"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/247"]}
tags: []
createdAt: "2026-11-01T02:18:21.543Z"
updatedAt: "2026-11-01T02:18:21.543Z"
---
Exploration as_nrwwyw9vk1 (Mara 1), 2026-11-01, main af85f2a. Direction: the "Fast" idea under ob_6j8s2588lp, i.e. why the check got slower.

## What the source says (CI logs)
12 green main runs, all attempt 1, 41247500767 … 41262429556 (2026-10-31 22:17Z to 2026-11-01 01:45Z), `check:` line from each check-job log:
- tests median 101.5 s (range 76–129 s); check total median 120 s (90–153 s).
- Baseline [dc_r5j4bdtmzo](../../report/2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md) (10-30, 12 runs): tests 76.5 s (58–93), total 94 s (73–116). So tests +33%, total +28%. Below the weekly watch's slowdown line (median >140 s) but trending up.
- Per workspace in run 41262429556 (vitest "tests" summed over workers): core 96 files / 602 tests / 101 s, server 44 s, runtime 41 s, cli 10 s, web 5 s, desk 2 s. The six workspaces run one after another (scripts/check.ts:46).

## What I measured (my desk, 2 vCPU)
- `openDb(":memory:")` = 51 ms (runs all 76 migrations); `World.open(":memory:")` = 58 ms.
- Instrumented migrate() over core's suite: **521 fresh databases, 65.5 s summed = 46% of core's 142 s test time.**
- Deserialising a migrated image (`new Database(db.serialize())`, 631 KB) = 0.47 ms, ~100× cheaper.
- Prototype (draft PR #247): openDb starts any new database (":memory:" or a missing file) from a once-per-process image of the migrated schema; migrate() still runs after it (no-op). Same tree with/without, 2 workers: **core 116.7 → 92.5 s wall, runtime 39.2 → 32.6 s, server 55.0 → 46.7 s** (−19% over the three). All 605/212/254 tests pass; full `npm run check` green on the branch (desk: tests 3m36s, the desk is slower than CI). New test core/test/db-schema-image.test.ts pins the image to the exact sqlite_master and schema_version of running every migration, WAL on a file, and that copies don't share rows.
- The old server run had 1 flaky failure (not reproduced with the change; not investigated).

## Inferred
- Every new migration makes every test that opens a database slower: the cost grows with migrations × tests, which is why the suite slows without anyone touching tests. The image removes the migrations term.
- Next biggest term is vitest "collect" (module import/transform): core 50 s, server 31 s, runtime 17 s summed on the desk. Untested levers: one root vitest run with `projects` (one pool, no six serial start-ups), `pool: threads`, or a lighter import graph for tests.

## Not known
- The CI gain: runner variance is ~1.6× on identical code, so it needs a median over ~10 main runs after merge.
- Whether production cares: a fresh production database is rare; for an existing file openDb is unchanged.
