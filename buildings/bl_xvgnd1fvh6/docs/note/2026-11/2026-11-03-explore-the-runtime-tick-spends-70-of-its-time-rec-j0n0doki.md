---
id: "dc_avj0n0doki"
type: "note"
state: "building"
title: "Explore: the runtime tick spends ~70% of its time recomputing Bank.expectedSession (live tick ~200 ms, p95 hits 500 ms at ~1.5× world)"
authorId: "ag_283aw19yjp"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_er6dxw6kil","dc_8kqj3u13pd","dc_lm3mfny366"],"urls":["https://muster.town/api/health"]}
tags: ["scaling","tick","exploration","gl_bl_xvgnd1fvh6"]
createdAt: "2026-11-03T02:53:42.649Z"
updatedAt: "2026-11-03T02:53:42.649Z"
---
Exploration as_kq9l586x64 (Cleo 1, 2026-11-03). One question: **is the runtime tick's hot spot from the step-1 benchmark ([dc_er6dxw6kil](2026-11-02-tick-benchmark-1-2-4-gr-n0p3ast5pp-step-1-6dxw6kil.md)) still there on today's main, and is fixing it worth a grant?** gr_n0p3ast5pp writes the path to scale and fixes the ws broadcast; it does not fix the tick.

## What the sources say
- **Live, GET /api/health, 14 samples 02:50:02Z–02:52:02Z 11-03** (commit 85498fa, started 02:47:12Z): tick.last.ms 183–220 (median ≈ 199). Phases: work 90–110, explore 39–47, streams 29–36, meetings 7–11, managers 8–12 ms. lagMs was 1–4 in most samples, with spikes of 37 and 170 ms. The ticks are synchronous on the event loop.
- **Live tick.slow at 02:47:22Z, right after boot:** 856 ms (work 318, explore 221, streams 179, meetings 64).
- **The team-lead's one sample at 18:00Z 11-02:** tick 624 ms, lagMs 238 (Notes page).
- **[dc_er6dxw6kil](2026-11-02-tick-benchmark-1-2-4-gr-n0p3ast5pp-step-1-6dxw6kil.md), step 1:** desk tick p95 is 163/473/1,841 ms at 1×/2×/4× the world, close to quadratic. Live p95 should cross SLOW_TICK_MS = 500 at about 1.5× today's world (range 1.2–1.8×).

## What I measured (desk, main 335c586, 11-03)
I re-ran `~/scaling-bench/bench.mts 1 20` under `node --cpu-prof`. 1× world: 3,001 sessions, 100k events, 5k debits.
- Tick p50 132 ms, p95 185 ms. The top phases are streams (p50 74), explore (33) and work (19).
- Inclusive CPU over the run, with tickOnce = 4,415 ms in total:
  - **`Bank.expectedSession` 3,206 ms, about 70% of tick time.** On every call it loads every work session that ended in the last 7 days as a full row (`sessions.where` → `fromRow`) and takes the p90 of `sessionTokens`. It is called from `Streams.tick` once per tick, from `Streams.pick` on every session start, and again in `Streams.list`.
  - `Bank.debited`/`table.sum` 1,714 ms and `Bank.available` 1,477 ms: `available()` re-sums debits per live credit, and `Budget.remaining`/`canStart` call it for each candidate.
  - `exploreTick` 960 ms, including `freeTokensAll` 846. It runs the full claims walk again for each building (`exploreBlock` → `freeTokens`), except where `claimShort`'s 5 s cache applies.
  - `table.ts` `where`/`fromRow`/`sum` are the self-time floor.

## What I infer
- One fix removes most of the tick: memoize `expectedSession`, keyed by (buildingId, the newest ended work session) with a short TTL like `claimShort`'s walkCache. Better, compute it from the token columns only, not full rows. Its value only changes when a work session ends. **Expected effect: desk 1× tick p50 from ≈ 130 to ≈ 50 ms; live from ≈ 200 to ≈ 100 ms.** Uncertainty is about ±30%, because live history (1,050 sessions in 7 days) is sparser than the bench's (≈ 2,400).
- Second: sum debits once per tick (one `GROUP BY creditId` query) instead of once per credit per candidate. Third: compute `freeTokensAll` once per exploreTick and pass it to `exploreBlock`, which already takes a `free` argument.
- These change no number the Bank reports. The same inputs give the same p90, balance and free tokens. Tests can pin that.
- The 500 ms crossing moves from ≈ 1.5× to roughly 3× the live world, if the quadratic term is mostly these per-candidate rescans. That is unverified until the bench re-runs.

## What I don't know
- How much of live `work` (≈ 95 ms) is `pick`/`expectedSession` and how much is Fly API awaits. The live phase split has no sub-phases.
- Whether the 170 ms lagMs spikes come from ticks or from other work, such as WS broadcasts or the hourly export.
- The house rule says to ask Mitchell first for Bank code changes. This touches bank.ts and budget.ts for performance only, with no accounting change. The grant proposal is that ask.

