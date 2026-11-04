---
id: "dc_8n3on7i7l6"
type: "note"
state: "building"
title: "Bank sheet build plan (gr_567tikzitl): file-level inventory, steps, before-measurements"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_zuh4oien9g"],"urls":[]}
tags: ["bank","ux","gr_567tikzitl"]
createdAt: "2026-11-03T22:52:08.965Z"
updatedAt: "2026-11-03T22:52:08.965Z"
---
Written 2026-11-03 at 1826430 (live), before the grant is funded, so the first fork starts from facts, not a re-read. Decided in 1:1 mt_qdt8elaktu (notes [dc_zuh4oien9g](../../meeting-notes/2026-11/2026-11-03-1-1-mitchell-and-nell-notes-h4oien9g.md)).

## Before (live 1826430, 1400×900, signed out, panel body 760 px high)
| tab | scroll px | screens | prose blocks* | words |
|---|---|---|---|---|
| Overview | 1,605 | 2.1 | 4 | 411 |
| Tokens & sources | 3,832 | 5.0 | 5 | 1,098 |
| Free tokens | 1,807 | 2.4 | 2 | 542 |
| Spending | 7,258 | 9.6 | 6 | 3,631 |
| Hosting | 977 | 1.3 | 3 | 304 |
*`p.muted`/`div.muted`/`.foot-note` over 60 chars, outside the Terms block. Donate section starts 1,397 px down Overview (picture mf_lp13m3tjub). Bank inputs: 18 rows, 15 cancelled, 1,288 px (mf_tihjpsddmr). Sources: 56 spend-rows. Spending: 1,550 spend-rows, Spend by goal alone 5,449 px. Earlier pictures: Overview mf_t1uwtl9c8f, Spending tree mf_r0e7vedcxc, title+tabs mf_vvibm28z5i, Hosting mf_kb6l6k1oe3. Script: ~/shots/before.mjs on Nell's desk (re-create from [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md) on a fork desk).

## Code inventory (read, then change)
- **Sheet shell to copy**: `packages/web/src/panels/GoalTreePanel.tsx` 41-120 (createPortal, `.ge-wrap`/`.ge`/`.ge-head`/`.ge-body`/`.ge-tree`/`.ge-detail`, Esc only when no side panel, backdrop click closes); `panelResize.tsx` `GeDivider`/`useGeDetailWidth`; CSS `styles.css` 800-871. Mount: `app.tsx` 226-235 (`goals` state kept while the side panel opens; `PanelHost` case "goals" returns null, line 209) and 318. Do the same for kind "bank": `PanelHost` case "bank" → null, a `bank` sheet state, `BankSheet` rendered beside `GoalTreePanel`. Everything that opens the Bank keeps working unchanged because the PanelRef kind stays "bank": `hud.tsx` 86/129/200, `PlanningPanel.tsx` 139, `map/renderer.ts` 56-60 (PLACE_PANEL bank → tab via `bankTabOf`), `route.ts` 13/36-43 (`#/bank`, old `#/finance`), `MeetingPanel.tsx` 239-240 (attach page "bank"), `state.ts` 16.
- **Tabs and room**: `packages/schema/src/index.ts` 2143-2190: `TILE.BANK_LEDGER..BANK_SERVER` (22-25), `BANK_FIXTURES` (door, pillars, vault, gold, map, `stations[]` with slug/tab/name/tile/cells/stand), `BANK_TABS = ["Overview", ...stations.tab]`, `bankTabOf`, `bankPlaces`. Sprites: `web/src/map/sprites.ts` 219 (vault), 264 (fountain, 2 tiles), 279 (ledger), 297 (rack). Core places from `bankPlaces` (world/layout.ts); roads use only `BANK_FIXTURES.door` (world/road.ts 79). Other `bank:free`/"Free tokens" mentions: `core/src/free-tokens.ts`, `core/src/prompts.ts`, `core/test/helpers.ts`, `core/test/lanes.test.ts`, `runtime/test/helpers.ts`, `web/src/format.ts`, `web/src/mock/server.ts`, `web/test/finance.test.tsx` (describe "free tokens", 313) and `bank-sign.test.ts`.
- **Tab bodies**: `BankPanel.tsx` (BankTab per tab; Balance table 63-78; BankSpending 109-153 with Drift + deaths), `BankFunding.tsx` (Donate 118, BuildingFunding 263 with the `showRetired` toggle at 313, BankInputs 320, BankStreamsSection 371), `BankFinance.tsx` (SpendRow/SpendingView 195-239, SourcesView 283-316, FinanceIntro 396, TokensView 422, ProjectionView 449, FlyView 342, FinanceFooter 480, FINANCE_TERMS/FinanceTerms 485-505), `FreeTokens.tsx` (BankFreeTokens 74, FreeTokensTree 99; keep FreeTokensLine/capText/desksText: the goal editor uses them), `GoalSpend.tsx` (SpendByGoal 31). No endpoint changes anywhere: the sheet reads the same `useFinance()` + `store.bank`; `npm run check:finance` stays the proof the numbers add up.
- **Tests**: `web/test/finance.test.tsx` renders `BankView` per tab with `renderToStaticMarkup` and asserts strings per tab: keep `BankView(tab, bank, fin)` as the one entry point so those tests move with the content; add one test per new behaviour (active-only default + toggle, drill-down path, Donate first, no Free tokens tab).

## Steps (one PR each, each shippable; pictures after each)
1. **Sheet shell** (kr_9xozv5d8gh): `BankSheet.tsx` + `bank-*` CSS copied from `ge-*`; left column = the tabs (vertical), centre = the current tab's tables, right sidebar = "About this tab" (that tab's prose: FinanceIntro, the section paragraphs, USD note, footer) + Terms + the selected row. Tab bodies unchanged inside. Esc/backdrop/× as the goal editor. 150-250k tokens.
2. **Donate first, chest, fountain gone, Balance line** (kr_00lym2zmif, kr_lq1qmywinq; one PR because both edit BANK_FIXTURES): station `{ slug: "donate", tab: "Donate", name: "Chest", tile: TILE.BANK_CHEST }` in the fountain's cells (2,5)-(3,5), stand (2,6) (no walkability change); fountain station and `FreeTokensTree` deleted; `BANK_TABS` = Donate, Balance (the vault, was Overview), Inputs (ledger), Spending, Hosting; `bankTabOf` default "Balance". Donate tab = the `Donate` form at the top (signed out: the sign-in line) and under it one table "Funding the town now": active inputs + building donations. Balance keeps its table plus one line "Free for exploration: N" (free.freeTokens; `freeTerms` in the sidebar). 150-250k.
3. **Active-only lists, row details in the sidebar** (kr_y7derda40x): Inputs = one table (input · from · size · credited · left · last draw · status) merging BankInputs + Streams + Sources' inputs, active by default, "Show N cancelled" (the BuildingFunding pattern); click a row → its dated credits in the sidebar (today's nested SourceInputLine). Building donations stay a small table under it. 100-150k.
4. **Spending drill-down** (kr_trhi5frg4k): `path: [buildingId?, grantId?]` state over the same `sp.rows` tree; level 1 = buildings (name · sessions · tokens · $ · share; Building funding's given/spent/left as columns), level 2 = that building's grants (+ grant line), level 3 = assignments; breadcrumb above the table. Spend by goal, Drift, deaths → a "Health" block in the sidebar or a second table behind a toggle, never below the drill-down. 150-250k.
5. Verify live after each: screenshots per [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md), the Before table above re-measured (target: every tab ≤ 1.5 screens at 1400×900, 0 prose blocks between rows), check:finance. ~100k.

If Mitchell counters at 600k: ship 1-3, checkpoint before 4.

## Open
- Teo's answer on the chest sprite and the fountain removal (asked 22:49Z, ms_5elv3fcnl9 → as_jqloithobc). If none by the time step 2 starts, go ahead: BANK_FIXTURES is schema, not UI/UX code.
- Raw→adjusted recompute: out of scope until Mitchell names the entries (decision 1).
