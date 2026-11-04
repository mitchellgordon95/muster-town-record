---
id: "dc_04orzov96w"
type: "report"
state: "building"
title: "gr_db6ofyd0yf step 2: missing creditId index was the cost; covering index (migration 089) cuts desk 2× tick p50 254 → 117 ms; PR #304 parked on CI"
authorId: "ag_i3xo7jbba8"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ur1qzaxafp","dc_g05085vk5z"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/304","https://muster.town/api/bank","https://muster.town/api/bank/streams","https://muster.town/api/health"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #304 (migration 089, covering index on bank_debits(creditId, tokens); desk 2× tick p50 254 → 117 ms) is parked on CI as as_fo0a9tdu70; its merge + live check run when CI finishes. Note gr_db6ofyd0yf is held at its checkpoint (rollup #35 pending), so that continuation stays held until Mitchell continues the grant. No rollup now: nothing of ours newly live since #35."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T17:03:16.708Z"
sessionId: "se_85wz1bzhj6"
assignmentId: "as_qizum6vt19"
costUsd: 1.9562089999999999
tokens: 97810
turns: 47
createdAt: "2026-11-04T17:03:04.542Z"
updatedAt: "2026-11-04T17:03:16.708Z"
---
## What I did
- Benched main on my desk (1× ×3, 2× ×1) and profiled at 2×.
- Found the cost: `bank_debits` has no index led by `creditId`. So every `debited("creditId = ?")` and the durable sum (`creditId IS NULL OR creditId IN (…)`) scanned the whole table on every `available`, `totals` or `unavailable` call.
- Added migration **089** `CREATE INDEX bank_debits_credit ON bank_debits(creditId, tokens)` (covering). No Bank code changed.
- Opened PR #304 (https://github.com/mitchellgordon95/muster-town/pull/304, head eea558ec), marked ready. It is parked on CI.

## Findings
- **I didn't use the planned GROUP BY.** I measured it on the 2× DB: it is a full scan, about 1.16 ms per call. With the index, the durable sum takes 0.04 ms.
- **Tests:** `test/bank-debits-index.test.ts`.
  - Both sums' query plans read the index, and neither scans the table.
  - Every Bank figure is identical with the index dropped (the old scans) and present: balance, usable, unavailable, available and remaining per building, inputBalance, freeTokensAll, summary and finance. Checked at 3 times.
  - The fixture covers expiring credits (one expired), a broken key, a cancelled key, an earmark, a credit with no debits, and a NULL-credit debit.
  - `test/helpers` `undoAdjustedTokens` now drops the index, because a 037 re-run drops `bank_debits.tokens`.
  - Core 725/725 passed after merging main; typecheck is green.
- **Migration number:** 088 was already taken on main (`088_schedule_taker`), so mine is 089. Re-check that it is still free before merging.
- **Desk bench, tick ms:**

| | p50 | p95 |
|---|---|---|
| 1× before (3 runs) | 67 / 65 / 62 | 106 / 94 / 99 |
| 1× after | 33 / 37 / 47 | 69 / 76 / 81 |
| 2× before | 254 | 309 |
| 2× after (2 runs) | 115 / 119 | 184 / 170 |

  - 2× p50 fell **−54 %** (stop line −15 %).
  - Streams p50 stays ~2–3 ms at 1×.
  - 2× phases: work 111 → 40 ms, explore 113 → 53 ms.
- **Live before (16:42:44Z, commit acf73450):**
  - expectedSessionTokens 123,877 (950 samples)
  - /api/bank: balance 3,234,205; durable −907,734 per building; credited 133,599,998
  - live tick 119 ms (work 53, explore 38)
  - The balance moves with every debit. The fixed figures to compare after merge are durable and credited.
- **After-profile at 2×, for step 3:**
  - `available` is still 32 % of the tick, but most of its `debited` share (24.5 %) is a bench artefact: all 10k bench debits sit on the single live credit. Live, the day's credit holds only that day's debits.
  - exploreTick is 30 % (freeTokensAll 15.5 %, exploreBlock 13.6 %).
  - spawnForks/forkableQueue is 25 %.
  - Step 3 should still pass one freeTokensAll through exploreTick, then do the full 1×/2×/4× bench into docs/scaling.md.
- **Next on resume:** if CI is green, check that 089 is still free on main, re-read the live figures, merge, and park on the merge sha. Then the live check: durable and credited unchanged (unless a credit or durable draw landed, named from events), expectedSessionTokens unchanged unless a session ended, and 12 tick samples. Topic page [dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md) is rewritten with this state.

## What I need from you
Nothing needed.
