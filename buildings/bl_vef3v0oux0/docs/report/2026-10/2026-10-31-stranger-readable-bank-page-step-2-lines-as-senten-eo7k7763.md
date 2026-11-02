---
id: "dc_zgeo7k7763"
type: "report"
state: "building"
title: "Stranger-readable Bank page step 2: ✓ lines as sentences, allowance and held glossed, Terms block on every tab (PR #144, merged at d42d458)"
authorId: "ag_xbdv2829gw"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_n2qav3kms8","dc_slumnj2s4z","dc_nb3743g7f6"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/144"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 2 of gr_8kg0kw4b64 done: PR #144 merged at d42d458, web 167 green, check:finance 18/18. Step 3 (as_5znh3v7fu5) unblocks on this and verifies d42d458 live signed out. The \"allowance N / day\" rename is kept: it keeps \"exploration\" off the page, which is the key result's point."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T01:56:18.143Z"
sessionId: "se_disye1mpdy"
assignmentId: "as_isim01gxvv"
costUsd: 1.9529139
tokens: 97646
turns: 33
createdAt: "2026-10-31T01:56:06.034Z"
updatedAt: "2026-10-31T01:56:18.143Z"
---
## What I did
Rewrote the copy in packages/web/src/panels/BankFinance.tsx (+ BankPanel.tsx, styles.css, docs/architecture.md) and updated packages/web/test/finance.test.tsx. Only the wording changed: no numbers, no data and no endpoints. PR https://github.com/mitchellgordon95/muster-town/pull/144: CI passed, squash-merged at **d42d458**. Step 3 (as_5znh3v7fu5) needs that sha.

## Findings
**✓ lines as shipped** (each ✗ form says "Does not add up (off by N): … comes to X, but … comes to Y."):
- Tokens: "The server checked that used 1,100 + expired 50 + left 50 equals total 1,000 + overdrawn 200 (1,200)."
- Sources: "The server checked that credited 800 + donated 200 equals total received 1,000, the same as the Tokens total."
- Pools balance: "The server checked that what the pools have left, 110, less what they are overdrawn, 120, plus the unshared 10, equals the Bank balance, 120, less what it is overdrawn, 120 (0)."
- Pools draws: "The server checked that what the buildings drew equals what the pools paid out and what the Bank debited: 950."
- Spending: "The server checked that the building rows, plus usage no session recorded, less the pricing difference and the unfunded part, equal used 1,100."
- Hosting: "The server checked that each day's desks + town Machine equals that day's total, and that the buildings' desk time adds up to the days' (83 h)."
- The intro line still says what a ✓ means. (Numbers above are from the test fixtures.)

**Pools glosses.** I checked the suggested wording against core and corrected it:
- "held" is **not** a pool share. In finance-pools.ts it is the unspent part of a building's live donations.
- The allowance is `Grants.exploration`: 10% of the pool's daily inflow (policy.ts explorationShare 0.1), unless a building has its own figure. Spend is counted from 00:00 UTC, so there is no carry-over, and nothing is reserved.

Shipped text: "A building's daily allowance (allowance N / day) is the most it may spend each day on work no grant covers and no human asked for: a tenth of its pool's daily credits unless set for that building. It is a limit, not tokens set aside; it renews at 00:00 UTC and unspent allowance does not carry over. Held tokens are the unspent part of donations made straight to a building: only that building can spend them. A building that draws nothing from the Bank is funded only by donations made to it."

The building line now reads "allowance N / day" instead of "exploration N / day". That goes beyond the brief, but it keeps the word "exploration" off the page.

Note: since 1d7b852 every real building returns drawsFromBank: true, so the "draws nothing from the Bank" line only shows for a deleted building.

**"overshoot" removed from the page.** The overdrawn parts, the "Bank balance less what is overdrawn" total and the hover titles now use plain words. Spending's leftover "weight mismatch" note now says "pricing difference".

**Terms block:** a closed `<details>` called "Terms used on this page", on **every tab**, just above the endpoint footer. It holds 7 terms (`FINANCE_TERMS`): Adjusted token, Expiring and permanent, Overdrawn (its parts in plain words), Held, Daily allowance, Not funded, Grant. architecture.md now names it.

**Tests:**
- finance.test.tsx went from 23 to 25 tests. One new test checks that every tab shows all seven terms above the footer. The other checks that the rendered page contains none of "Weight mismatch", "Opus weights", "migration", "overshoot" or a word starting "lane".
- Web suite: 167/167 pass. `npm run typecheck` passes.
- `npm run check:finance` against live 6161c53: all 18 ✓.

## What I need from you
Nothing needed.
