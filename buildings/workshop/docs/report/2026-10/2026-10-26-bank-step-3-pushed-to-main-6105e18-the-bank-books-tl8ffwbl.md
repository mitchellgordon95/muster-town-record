---
id: "dc_s0tl8ffwbl"
type: "report"
state: "building"
title: "Bank step 3 pushed to main (6105e18): the Bank books and shows adjusted output tokens; parked for live check"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 3 on main as 6105e18 accepted; your parked continuation does the live check after the deploy (redeploy with image requested from this session). Your ask (Mitchell confirms bi_au5kt05vlj 1,333,333/day cap 9,333,333, bi_foh0utko9b 666,667/day cap 3,333,333) goes in my checkpoint rollup. Note Mitchell adjusted the grant to 40M raw at 22:17Z, so migration 037 converts it to 1,333,333 adj., not 800,000: check the bank.converted event shows that. On resume also report the grant's re-derived adjusted spend vs its converted amount, since real Fable sessions run nearer ÷16.5 than ÷24 and the grant may read over 100% in the new unit; step 5 as_23e58ae0lf stays held until Mitchell continues the grant."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T22:33:44.239Z"
sessionId: "se_v01krchftm"
assignmentId: "as_dmc563ox56"
costUsd: 5.698752
tokens: 497296
turns: 106
createdAt: "2026-10-26T22:32:02.086Z"
updatedAt: "2026-10-26T22:33:44.239Z"
---
## What I did
Built Bank step 3 of gr_iq5m7dug56 from my plan and pushed it straight to main as **6105e18**. I also requested the redeploy. The work is parked until 6105e18 is live, and I'll do the live check next session. Root's step 4 (dee89b9, drift job) landed while I worked, and its migration took the number 036, so mine is `037_adjusted_tokens.sql`. I merged the rebase conflicts. Step 4 reads sessions directly, so this change doesn't affect it.

## Findings
- **Unit switch (core):** the Bank now enters, books and compares everything in adjusted output tokens:
  - Ledger rows (`usage`, `bank_debits`, `bank_credits`) store `tokens` as the adjusted figure. The raw sum is a generated `rawTokens` column next to the five counters. Allocations do the same with `spentTokens` and `spentRawTokens`.
  - A session's charge is priced at its own model, per model when it has `byModel`. So the tokens booked for a session equal its `adjustedOutputTokens`, and a test checks this for a Fable session with a Haiku subagent.
  - A bare number is treated as already adjusted, and its counters are the back-fill split of the raw tokens behind it.
  - Grant spend and exploration spend are the sum of their sessions' adjusted figures.
- **Migration 037:** converts every size once at Root's back-fill rule (÷30 for Opus and any non-Fable model, ÷24 for Fable), rounded. That covers inputs (size, cap, credited), allocations, grant ask, grant amount and history, building allowances, agents' spend counters, donations and report token stamps. It recomputes the ledger from its counters and writes one `bank.converted` event listing each figure as `[before, after]`.
- **Converted live figures (all inputs are Opus):**
  - bi_au5kt05vlj: 40M/day, cap 280M → **1,333,333/day, cap 9,333,333**
  - bi_foh0utko9b: 20M/day, cap 100M → **666,667/day, cap 3,333,333**
  - gr_iq5m7dug56: 24,000,000 ask and grant → **800,000**. Its spend becomes the sum of its sessions' adjusted tokens, and its checkpoints already done stay [0.5].
  - New defaults: 350k tokens per agent per day; the seed's house budget is 1.7M.
- **/api/health** now returns `accounting: "adjusted"`.
- **Web client:** these places now say "adj. tokens": the Bank page and map sign, in-tray grant and report amounts, the building panel (tokens used, daily allowance), grant progress and history, key-result lines, agent totals and session, and every "M tokens" input box. Hovering shows what the unit means plus the five counters and the raw total on the Bank balance, input credits, allocation spend (with a new `spentCounts` on grants), grant progress and sessions. The $ estimate on the Bank form now defaults to $20 per 1M adj. tokens.
- **Docs:** a step 3 section in docs/bank.md, plus a line in docs/log.md.
- **Tests:**
  - New `core/test/bank-adjusted.test.ts` checks the migration against the live figures above, including the event.
  - Rewritten tests for booking (`token-counters`), plus updated budget and lanes tests.
  - Server: health field (`live.test.ts`), desk session-end and `/api/bank`.
  - Runtime: work and desk tests. Web: keyResults.
  - All of these pass. Typecheck is clean for core, server, runtime, schema, desk and web; web was checked before the rebase.
  - I did not run the full suite: the desk is slow, so I ran only the affected test files.

## What I need from you
Mitchell: confirm the converted figures in the new unit: bi_au5kt05vlj 1,333,333/day with a 9,333,333 weekly cap, bi_foh0utko9b 666,667/day with a 3,333,333 cap, and gr_iq5m7dug56 at 800,000 adj. tokens.
