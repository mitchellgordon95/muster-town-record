---
id: "dc_k0cf1z02jt"
type: "report"
state: "building"
title: "Accounting pools core on feature/accounting-pools @ 990d191 (ready for Lena's UI)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T22:56:18.348Z"
sessionId: "se_zpot7cul5n"
assignmentId: "as_47d5krpewr"
costUsd: 2.320293500000001
tokens: 112604
turns: 44
createdAt: "2026-10-20T22:53:01.441Z"
updatedAt: "2026-10-20T22:56:18.348Z"
---
## What I did
I built the core half of accounting pools on a new branch, `feature/accounting-pools`, cut from origin/main. That covers the schema, migration 023, the pool math, the API, the tests and the docs. I also made the smallest web edits needed to compile. The branch is pushed, but not to main and with no redeploy, as the assignment said. Branch head: **990d191dcf0939f5c104c922b76b3d415ccd273b**. I sent Lena the API shape.

How I checked it: `npm run typecheck` passes in every package, and `npm test` passes everywhere (core 195/195, server REST 56/56, all other packages green).

## Findings
**Pool math and draws**
- A pool has `{id, name, pct | null, createdAt}`, stored in `bank_pools`.
- Explicit shares come first and can't total more than 100.
- Pools without an explicit share split what's left equally. Spec decision: an empty pool gets 0%, so no share sits unused.
- A building can draw what's left in its pool. Buildings in the same pool share it first come first served.
- Draw order, failover and the per-agent daily cap are unchanged.
- The Town Hall stays in General but draws nothing from the Bank.
- Each debit now records its `poolId` (the pool charged) as well as its `buildingId` (who spent it). After a building moves, what it already drew stays charged to the old pool.

**Building ↔ pool**
- `Building.poolId`: null means General (`DEFAULT_POOL_ID = "general"`). General can't be deleted.
- `PATCH /api/buildings/:id {poolId}` takes effect at once and is admin only. Other fields in the same PATCH still need `building.manage`.

**Migration 023**
- Creates General and puts every building in it.
- Spec decision: a building that had an explicit share gets its own pool, `pool-<buildingId>`, with that %, so no one's draw changes. If no shares were set, everything ends up in General.
- Drops `bank_shares`, adds `poolId` to existing debits and fills it in.

**API**
- `GET /api/bank/pools` → `{pools}`
- `POST /api/bank/pools {name, pct?}` → 201 `{pool, bank}`
- `PATCH /api/bank/pools/:id {name?, pct?: number|null}` → `{pool, bank}`
- `DELETE /api/bank/pools/:id` → `{bank}`. Only works on an empty pool, and never on General.
- `PUT /api/bank/shares/:id` and `SetBankShareInput` are removed; the old endpoint now returns 404.

**`GET /api/bank` summary**
- New: `pools: [{id, name, pct, explicit, isDefault, buildings: [{buildingId, name}], expiringTokens, durableTokens}]`.
- `buildings[]` gains `poolId` and `poolName`. Its `pct` and `explicit` are now the pool's, and the token fields show what's left in the pool. The Town Hall shows pct 0.

**Tests added**
- Equal and explicit split, including the 100% cap and empty pools.
- Delete only when empty; General can't be deleted.
- First come first served within a pool; the Town Hall draws nothing.
- A move takes effect at once and is admin only.
- Summary shape.
- Migration from a pre-023 database, plus a fresh town.
- REST endpoints.

**Web (minimal, for Lena)**
- `api.ts` has the new types plus `createBankPool`, `updateBankPool`, `deleteBankPool` and `setBuildingPool`.
- The mock implements pools.
- `BankShares` is a placeholder that edits the pool's share.

## What I need from you
Nothing needed.
