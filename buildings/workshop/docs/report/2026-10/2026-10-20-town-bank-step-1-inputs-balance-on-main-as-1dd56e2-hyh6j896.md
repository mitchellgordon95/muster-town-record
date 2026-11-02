---
id: "dc_nwhyh6j896"
type: "report"
state: "building"
title: "Town Bank step 1 (inputs + balance) on main as 1dd56e2; redeploy started"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T17:54:00.693Z"
sessionId: "se_3zykzjae1y"
assignmentId: "as_a2cioi39a8"
costUsd: 1.1953357000000002
tokens: 54698
turns: 34
createdAt: "2026-10-20T17:15:49.214Z"
updatedAt: "2026-10-20T17:54:00.693Z"
---
## What I did
Root's drain-then-restart redeploy was already on main (280d204), so I built step 1 of the Bank: inputs and the balance. Per the standing rule, I pushed straight to main as **1dd56e2** (no PR) and then started a redeploy, which drains running sessions before it restarts.

## Findings
- **Inputs.** A `BankInput` has a label, a source (`api-key` or `subscription`), a model, a token amount, and a recurrence: `once`, `daily`, `weekly` or `monthly`.
  - The API key goes in a secret column. The API never returns it; I checked this in the REST test.
  - A one-time input credits when it's added.
  - A recurring input credits only on its renewal date (`nextCreditAt`). It pays once per renewal, so if the server is down for several renewals it doesn't pay them all at once afterwards.
  - Only an admin can add a subscription input (Mitchell's own plan). It credits daily: the smaller of the daily amount and whatever is left of `weeklyCapTokens` over the last 7 days.
  - Cancelling an input (owner or admin) stops future credits and deletes the stored key. Tokens it already credited stay in the Bank.
- **Balance.** Every credit is written as a row in a new `bank_credits` table (migration 012) and logged as a `bank.credited` event. The balance is the sum of those rows. The runtime credits any due inputs on every tick.
- **API.** `GET /api/bank` returns the balance, total credited, daily inflow and the list of inputs. `POST /api/bank/inputs` adds an input. `DELETE /api/bank/inputs/:id` cancels one.
- **Not built yet.** Buildings still run on their own allocations and don't draw from the Bank. The stored keys aren't used for sessions yet. Those come with step 2 (each building's % share), then step 3 (the Town Hall view).
- **Verified.** `npm run typecheck` is clean and all package tests pass (core 114, plus server, runtime and the rest). The new tests are `packages/core/test/bank.test.ts` (one-time, recurring, subscription cap, permissions) and a bank block in the server REST test. I updated the v1.1 migration test to also drop the new tables. `docs/architecture.md`, `README.md` and `docs/log.md` are updated.

## What I need from you
Nothing needed.
