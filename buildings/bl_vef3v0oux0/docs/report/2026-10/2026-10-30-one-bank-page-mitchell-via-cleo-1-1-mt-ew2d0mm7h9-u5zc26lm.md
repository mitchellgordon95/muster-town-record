---
id: "dc_i9u5zc26lm"
type: "report"
state: "building"
title: "One Bank page (Mitchell via Cleo, 1:1 mt_ew2d0mm7h9): the Finance page's sections now sit on the Bank page, #/finance redirects to #/bank; on main at 8305070, fork queued to verify live"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["mt_ew2d0mm7h9","dc_nb3743g7f6","dc_xeui247glt","dc_a0q82pir2r"],"urls":["https://github.com/mitchellgordon95/muster-town/commit/8305070dd83100f1e04b298af5e7f82091e4a8f8"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Clean: 8305070 on main, 150/150 web tests, docs and topic pages rewritten, Cleo told. The live check (as_quzjqop0di) is already queued on deploy 8305070; its report decides the rollup. Pools-merge follow-up stays unasked unless Mitchell wants it."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-30T18:35:41.856Z"
sessionId: "se_3zobopc079"
assignmentId: "as_ik5bto58h2"
costUsd: 6.1938622500000005
tokens: 123877
turns: 54
createdAt: "2026-10-30T18:35:21.990Z"
updatedAt: "2026-10-30T18:35:41.856Z"
---
## What I did
Mitchell asked (via Cleo, 1:1 mt_ew2d0mm7h9) for one Bank page: the token sections and "Hosting (Fly.io)" together, the separate Finance page gone or redirecting. Done and pushed straight to main at 8305070 (the pre-made PR branch is unused; CI deploys main). Cleo told (ms_8ranlj74ud). A fork assignment (as_quzjqop0di, directed, waits for the deploy of 8305070) verifies it live: headings in order, the redirect, `npm run check:finance`, row layout at 1000/1400 px, and one cropped picture for the rollup.

## Findings
- **The page.** `packages/web/src/panels/BankPanel.tsx` now lays out one public page, "The Bank", in this order: unit line → Balance → Tokens (✓) → Next 30 days → Top contributors → Donate → Bank inputs → Sources (✓) → Pools (editable) → Building funding → Pool balances (✓✓, the finance pools section, retitled so the two don't collide) → Spending (✓) → Hosting (Fly.io) (✓, US dollars) → Drift → Out-of-tokens deaths and the cap → footer naming the endpoints. The finance views moved from `FinancePanel.tsx` to `BankFinance.tsx` (TokensView, ProjectionView, FinanceIntro, FinanceFooter, `useFinance` loader); the old `/api/bank` "Bank pools" fallback table is dropped since the editable Pools table is on the same page.
- **Routes.** Panel kind `finance` is gone. The HUD's "$" opens the Bank; `#/bank` is its hash; the old `#/finance` opens the Bank and the address bar rewrites to `#/bank` (checked in the mock client with headless Chromium: hash `#/bank`, 13 headings in the order above). A meeting's presented page `finance` opens the Bank (web side only; `core/src/meetings.ts` PAGES still accepts the name, untouched).
- **API.** Nothing changed: `/api/bank`, `/api/finance`, `/spend`, `/sources`, `/pools`, `/fly` as before; `npm run check:finance` unaffected. Prod's desk cap and per-session sizing untouched.
- **Checks.** `npm run check --fast` green: docs 1 s, typecheck 11 s, tests 24 s; full web suite 150/150 (finance.test.tsx 23 tests now render `BankView`, one asserts the section order). docs/manual.md sits at ≈1,894 words against the test's 1,900 cap, so I trimmed the Bank bullet; the next manual edit must trim too.
- **Docs.** manual.md (Funding bullet), architecture.md (`/api/finance` paragraph), invariants/bank.md, meetings.md (page `finance`), log.md. Topic pages [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md) (now "The Bank page…") and [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md) rewritten.
- **Open question for the layout, not acted on:** the editable Pools table (shares, members, can-draw) and Pool balances (accounting with ✓ lines) are two adjacent sections with Building funding between them. Merging them into one is a follow-up if Mitchell wants it.

## What I need from you
Nothing needed.
