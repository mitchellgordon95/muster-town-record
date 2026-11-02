---
id: "dc_0q4mlk2wuh"
type: "note"
state: "building"
title: "Abstraction sweep 1: candidates"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["kr_doa59kdway","abstraction-sweep"]
createdAt: "2026-10-28T17:37:01.986Z"
updatedAt: "2026-10-28T17:37:01.986Z"
---
Sweep of `packages/` at main 6af7714 (2026-10-28) for kr_doa59kdway. Method: grep for known shapes (fetch/JSON parse, WHERE builders, admin checks, day math, formatters, retries/sleeps) plus a home-made duplicate-window detector (normalised 4–5 line windows across all non-test .ts/.tsx; /home/agent/tools/dupes.py on Finn's desk). jscpd wasn't reachable. Nothing was consolidated. Token estimates are guesses from similar past PRs (±50%). Two kinds of finding: plain duplication, and **drift** (copies that have already diverged). Drift is the stronger reason to consolidate.

## Ranked candidates

### 1. ★ Desk contract copy → `@muster-town/schema` (drift found)
- Occurrences: `packages/desk/src/contract.ts:8-71` (DeskWorkspace, DeskBrief, DeskActivityInput, DeskControl, DeskSessionEndInput) duplicates `packages/schema/src/index.ts:1585-1653`. The file says "TODO: switch to @muster-town/schema when exported"; they are exported now. Importers: `desk/src/run.ts:11`, `desk/src/town.ts:2`, `desk/src/workspace.ts:9`.
- **Drift:** the server sends `interrupts[].now` (`server/src/routes/desk.ts:60`), and the desk copy declares it, but schema's `DeskControl` doesn't, so anything parsing with schema drops `now`. Nullability and defaults on `DeskSessionEndInput` also differ.
- Abstraction: delete contract.ts and import from schema. Add `now` to schema `DeskControl`. Keep the desk's parse lenient (passthrough views): the desk image can run a different commit than the server.
- Removes: 1 file, ~60 lines, 5 schemas.
- Risk: low. Needs a desk image rebuild (`redeploy image=true`). No Bank, schema-migration or DB change.
- Estimate: ~40k tokens.

### 2. ★ Dynamic SQL WHERE builder → `core/src/table.ts`
- Occurrences (hand-rolled `where.push; params.push; where.join(" AND ")`): `core/src/events.ts:57-67`, `core/src/grants.ts:246-250`, `core/src/skills.ts:133-136`, `core/src/verbs/docs.ts:59-63`, `core/src/verbs/docs.ts:75-83`, `server/src/routes/docs.ts:30-35`, `server/src/routes/docs.ts:108-115`. That's 7 sites and ~25 push lines.
- Abstraction: `whereOf({col: value|undefined, ...}, extra?) → {sql, params}` (skips undefined, handles `IN (...)` for arrays) next to `Table.where()`. It could also take `limit` as a bound param; today every `LIMIT ${n}` is interpolated, though each value comes from a zod int.
- Risk: low. Core storage layer, read-only queries, no schema change.
- Estimate: ~35k tokens.

### 3. ★ Admin checks → `core/src/permissions.ts`
- Occurrences of `permissions.isAdmin({ kind: "user", id })`, mostly followed by a hand-written `AppError("forbidden", "Only an admin…")`: `server/src/routes/town.ts:109, 210, 322`, `server/src/routes/agents.ts:48`, `server/src/routes/secrets.ts:15`, `server/src/app.ts:141, 170`, `server/src/auth/session.ts:122`, `core/src/kpis.ts:42`, `core/src/bank.ts:272, 298, 441`. That's 12 sites. "Admin or has permission X" also appears at `town.ts:283, 389`.
- Abstraction: `permissions.isUserAdmin(userId)` and `permissions.requireAdmin(holder, message)`, which throws `forbidden`. Today some sites pass 403 explicitly and some rely on the default.
- Risk: low to medium. The 3 sites in bank.ts are Bank code: leave them out or ask Mitchell first.
- Estimate: ~30k tokens.

### 4. Desk SDK helpers copy → one module (drift found)
- `packages/desk/src/sdk.ts:1-119` copies `packages/runtime/src/sdk.ts:1-121` (Sdk types, realSdk, userMessage, InputChannel, LooseMessage, Usage, noUsage, usageOf, plusUsage, blocksOf). That's 63 matching 5-line windows, the largest duplicate in the repo.
- **Drift:** the desk's `LooseMessage` has `error?: string` and the runtime's doesn't.
- Abstraction: the runtime imports from `@muster-town/desk/sdk` (adding desk as a dependency), or the pure parts move to schema with a type-only SDK import.
- Removes: ~110 lines.
- Risk: medium. `usageOf`/`plusUsage` feed token accounting (move only, but ask Mitchell per the merge rule). Needs a desk image rebuild.
- Estimate: ~50k tokens.

### 5. Town HTTP client → schema `townRequest`
- Occurrences: `cli/src/client.ts:4-27`, `web/src/api.ts:451-466`, `desk/src/town.ts:35-64`. Raw fetches that bypass HttpApi: `web/src/auth/auth.tsx:32, 54` and `web/src/home/StartCard.tsx:20, 23, 94`.
- **Inconsistent:** the CLI and web read the server's `{error, code}`, while the desk throws raw text. Only the desk retries. None has a request timeout (only `desk/cli.ts:61` and `runtime/desk/fly.ts:61` set `AbortSignal.timeout`).
- Abstraction: `townRequest({base, token, method, path, body, timeoutMs, retries})` in schema; each caller wraps the error in its own class.
- Risk: low to medium. It spans the web, CLI and desk; StartCard/home belong to Onboarding.
- Estimate: ~50k tokens.

### 6. Response view types hand-copied in `web/src/api.ts` → schema type-only `views.ts`
- 13 types (web line → core): SpendNode 110 → `finance-spend.ts:18`, FinanceSpend 122 → `:31`, HeldByAuth 88 → `bank.ts:162`, BankPoolSummary 129 → `bank.ts:127`, BankBuildingShare 140 → `bank.ts:143`, BankContributor 141 → `bank.ts:165`, BankDeaths 175 → `caps.ts:21`, BankCapState 179 → `bank.ts:213`, DriftRow 184 → `drift.ts:12`, BankDrift 188 → `bank.ts:233`, FamilySpend 36 → `forks.ts:253`, ForkSummary 39 → `forks.ts:188`, ReportChain 56 → `forks.ts:204`. The web can't import core (sqlite).
- Risk: medium. Mostly Bank and finance types (type-only), so ask Mitchell.
- Estimate: ~45k tokens.

### 7. Day/time math → `core/src/util.ts`
- `DAY_MS = 86_400_000` is defined 4 times: `core/bank.ts:12`, `finance.ts:4`, `transcripts.ts:23`, `kpis.ts:10`. The literal appears inline at `drift.ts:36, 79`, `caps.ts:44, 74`, `skills.ts:113`, plus `media.ts:54` and `server/backup/index.ts:29`.
- `utcDay` exists (`drift.ts:35`), but `.toISOString().slice(0,10)` is still inline at `caps.ts:74`, `backup/index.ts:48, 142`, `routes/town.ts:364`.
- Abstraction: `DAY_MS`, `utcDay`, `daysAgoIso(n, now)`. Removes ~15 sites.
- Risk: low (bank and finance files lose only a local constant).
- Estimate: ~20k tokens.

### 8. Debounced draft-preview store (web map editors)
- `web/src/map/layoutEdit.ts:100-127` and `web/src/map/townPlan.ts:160-188` have the same save flow and the same 120 ms debounced `check()` with seq-based stale drop.
- Abstraction: `makeDraftStore({preview, save})` in `web/src/map/draft.ts`. Risk: low, web only.
- Estimate: ~25k tokens.

### 9. SDK message-stream reducer
- `runtime/src/session.ts:252-280`, `desk/src/run.ts:257-295` and `runtime/src/sdk.ts:178-187` all walk blocks, take usage on `result`, and pick finalText and error.
- **Divergence:** the host takes error from `m.errors || subtype`; the desk takes it from the result text and classifies SPEND_LIMIT itself (`run.ts:310`). On the host path only `core/ops.ts:518`'s fallback catches cap deaths. I haven't checked whether host sessions miss `bank.cap` events.
- Risk: high (runtime core, token accounting, failover). Do it after #4. ~90k tokens.

### 10. Small web copies (batch)
- `labSize` is copied in `web/src/map/townPlan.ts:35` from `core/src/world/layout.ts:37`.
- There are two different `usd` formatters (`panels/ui.tsx:21`, `panels/BankFunding.tsx:47`).
- `toLocaleString("en-US")` is written inline 15 times (8 in BankPanel.tsx), with local helpers at `FinancePanel.tsx:14` and `map/overlay.ts:304`.
- `COUNT_LABELS` in `web/src/format.ts:13` re-lists schema `TOKEN_KINDS`.
- Risk: low, cosmetic. ~20k tokens.

## Top 3 first
1. **#1:** the cheapest, the file's own TODO asks for it, and it fixes real drift.
2. **#2:** 7 sites into a core layer, low risk.
3. **#3:** 12 sites, one consistent 403; server sites first, the bank.ts ones after Mitchell's word.

#1–#3 come to ~105k tokens. #4 is the biggest duplicate but moves token-accounting code, so it goes fourth, after Mitchell agrees. #1–#8 total ~295k.

## Checked, already shared (not candidates)
- Error→HTTP mapping: `AppError` plus the `app.ts:113` handler.
- Body/query parsing: `parse()` in `server/src/context.ts:104`.
- Web loading: `useLoad` (30 uses).
- IDs and time: `newId`/`nowIso`.
- `sleep` is defined 3 times in packages that share nothing below schema; too small.

