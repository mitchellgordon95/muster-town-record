---
id: "dc_w8ibo8rl1z"
type: "report"
state: "building"
title: "Bank step 1 (five token counters) pushed to main bdc44f0; parked for the live check"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 on main at bdc44f0 (five counters, migration 034 generated sums, back-fill output = raw × (1/ratio − w)/(1 − w)); all suites pass; redeploy with image requested. Continuation does the live check once bdc44f0 is live. Step 2 (as_o7tti8xucf) builds on it."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T20:28:56.989Z"
sessionId: "se_5dny5mt9gn"
assignmentId: "as_tpm63840n3"
costUsd: 2.4858925000000003
tokens: 168613
turns: 56
createdAt: "2026-10-26T19:50:25.513Z"
updatedAt: "2026-10-26T20:28:56.989Z"
---
## What I did
I finished Bank step 1 from WIP f03ea13 and pushed it straight to main as **bdc44f0** (branch agent/root/finish-bank-step-1-from-wip-f03ea13-fix- too). No PR, per the standing rule. The 11 core tests that broke are fixed, and the runtime and desk now carry the five counters. I added docs/bank.md and new tests. `npm run typecheck` is clean, and every suite passes: core 277, runtime 122, server 75, web 61, desk 22. I requested a redeploy with image=true, because the desk code changed and the desk image has to be rebuilt before it posts real counters. The work is parked until bdc44f0 is live.

## Findings
- **Migration 034** (`034_token_counters.sql`):
  - `sessions`, `usage`, `bank_debits` and `bank_credits` each gain `input`, `output`, `cacheRead`, `cacheWrite5m` and `cacheWrite1h`. `allocations` gains `spentInput` … `spentCacheWrite1h`.
  - `tokens` and `spentTokens` are now SQLite generated columns (the sum of the five), so a raw total can't drift from the counters.
  - Pool balances are still credits minus debits. Bank inputs and allocation sizes stay raw until step 3.
- **SDK fields read** (`sdkTokenCounts` in packages/schema/src/tokens.ts, used by both the desk and host sessions):
  - Per model from `modelUsage[model]`: `inputTokens`, `outputTokens`, `cacheReadInputTokens`, `cacheCreationInputTokens` (cumulative per query).
  - The 5m/1h split of cache writes comes from `usage.cache_creation` (`ephemeral_5m_input_tokens`, `ephemeral_1h_input_tokens`), applied as a ratio. **If that split is missing or zero, every cache write counts as 5m.**
  - With no `modelUsage`, it reads `usage.input_tokens`, `output_tokens`, `cache_read_input_tokens` and `cache_creation_input_tokens` under the model "unknown".
  - The desk posts `counts` and `byModel` to session-end. A desk without the update posts only `tokens`, and the server splits it with the back-fill rule.
- **Back-fill rule:** output plus cache read only, chosen so that step 2's adjusted value comes out at exactly raw/ratio.
  - `output = round(raw × (1/ratio − w)/(1 − w))`, `cacheRead = raw − output`.
  - Opus and any non-Fable model: ratio 30, w 0.01, so output is 2.357% of raw. Fable: ratio 24, w 0.005, so output is 3.706%.
  - Example: 30,000 raw on Opus → 707 output + 29,293 cache read = 1,000 adjusted.
  - Rows with no model (usage, debits, allocation spend) count as Opus; a credit uses its input's model.
- **Events:** `session.ended` carries `model`, `tokens`, the five counters and `byModel`. `bank.input` and `bank.credited` carry the five.
- **Tests:** debits plus allocation spend equal the charge for each kind, and raw totals are unchanged. Migration 034 back-fills the usage ledger (4,300 → 101 output + 4,199 cache read). New test files are core/test/token-counters.test.ts and runtime/test/usage.test.ts, and server/test/desk.test.ts has a new case.
- What a token is worth hasn't changed (that's step 2), so every Bank total should read as before.

## What I need from you
Nothing needed.
