---
id: "dc_up4ketree0"
type: "note"
state: "building"
title: "Topic page text: Bank and token accounting"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["topic-page-text","forks-step-8"]
createdAt: "2026-10-28T19:24:10.600Z"
updatedAt: "2026-10-28T19:24:10.600Z"
---
State on 2026-10-28 ~19:30 UTC, main 869f76d (live). Spec: docs/bank.md. Grant gr_iq5m7dug56 (kr_vyrhhiyotb).
- **Five counters.** Migration 034_token_counters.sql: input, output, cacheRead, cacheWrite5m, cacheWrite1h; `tokens`/`spentTokens` are generated sums. schema/src/tokens.ts: TOKEN_KINDS, splitRaw, sdkTokenCounts, addUsage. Desks post the five + `byModel` on session end; bank.input / bank.credited events carry the five.
- **Back-fill** (old sessions with a bare `tokens`): output = raw×(1/ratio−w)/(1−w), rest cacheRead; Opus 30/0.01, Fable 24/0.005. Finance step 2b (f4499df): weightMismatch re-splits only migration-034 back-fills at the Opus ratio.
- **Adjusted output tokens** = what the Bank books. core/src/bank.ts TOKEN_PRICES ($/MTok, list prices) → tokenPrices / tokenWeights / adjustedOutputTokens. Opus 5.5 $4 in / $20 out / $0.2 cache read / $5 cw5m / $8 cw1h; Fable 5.1 $10/$50/$0.25/$12.5/$20. Unknown model → Opus 5.5 price plus a warning event. GET /api/health `accounting` shows the mode.
- **Calibration** (live data, 2026-10-26): sessions with real counters, adj × output price / costUsd median 1.019 (range 1.000–1.043, n=7); back-filled ones 0.69 (0.34–2.02, n=166), so only real counters are trustworthy. A desk sample after the 10-27 desk image push: ratio ≈1.00. Desks use the 1h cache, so cacheWrite5m = 0 is normal.
- **Who pays.** Bank.grantKeyInput(grant): the grant's fundedWith input when it is an api-key input with a key, not cancelled, balance > 0. runtime/src/session.ts fundingForSession uses that key for assignment sessions on the grant (host and desk; key passed per session in desk env); session.started payload gets inputId + grantId. Charging: drawFromInput debits the input first, then the pool. Meetings/chat (no assignment) still use fundingFor (pool). Test runtime/test/member-key.test.ts.
- **Forks family spend**: core/src/forks.ts familySpend = SUM over the manager and rows with forkOf = manager; GET /api/agents/:id/forks returns `family`. The daily cap counts the whole family (budget.ts familyCap).
- Bank or token-accounting changes need Mitchell's OK first (dc_xsrxxbfa7i).

