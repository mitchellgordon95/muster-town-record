---
id: "dc_fuyoi9k2ty"
type: "report"
state: "building"
title: "Recurring API-key donations limited to N credits: PR #216 open, parked on CI"
authorId: "ag_1x1ckderkf"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #216 (recurring API-key donations limited to N credits) is Mitchell's ask from 1:1 mt_p3ge56kg03 (notes dc_dw0izucnip), so the Bank-code ask-first is satisfied; the merge continuation as_1l9kmn00ct is already parked on {pr:216} and re-checks the migration number (main moved to cbe1bf1 since the push: 01220ca Bank.debited in SQL, Teo's #209). When it merges: live picture, rewrite dc_pnarp2er0m and dc_tkzoy81p4b. Goes into the next rollup with PR #202 under \"Your call: Bank code, asked for in the 1:1\"."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T22:13:36.597Z"
sessionId: "se_orzlox6r1l"
assignmentId: "as_v143vxiefm"
costUsd: 1.7300146999999995
tokens: 86501
turns: 42
createdAt: "2026-10-31T22:10:37.175Z"
updatedAt: "2026-10-31T22:13:36.597Z"
---
## What I did
Built Mitchell's plan from 1:1 mt_p3ge56kg03 as one PR: https://github.com/mitchellgordon95/muster-town/pull/216 (draft; CI running). Typecheck passes, core tests pass (580/580), web tests pass (208/208). I took a picture of the form on the local mock server (below). It is not merged or live yet.

## Findings
- **Schema:** migration `074_bank_input_credits_left.sql` adds two nullable columns to bank_inputs, `creditsTotal` and `creditsLeft`. Null means "until I cancel", so existing inputs are unchanged. The highest migration on origin/main was 073 when I pushed.
- **Core:** `AddBankInput.times` (1 to 1,000) is accepted only for a recurring API-key input. A one-time input or a subscription refuses it.
  - The credit made when the input is added counts as credit 1 of N.
  - `creditDue` counts `creditsLeft` down. At 0 it sets `nextCreditAt` to null; the input stays listed and is not cancelled.
  - `dailyInflowOf` (finance.ts) counts a limited input as min(creditsLeft, 30 / period) × tokens / 30. The same function feeds GET /api/bank `dailyInflowTokens` and /api/finance `projection.dailyInflow`, so the two still match.
  - New test in bank.test.ts covers: N=1 behaves like once; N=3 daily credits 3 times and stops (9,000 credited, still listed); inflow per day goes 200 → 100 → 0 and projectedInflow30d is 6,000; a 100-credit daily input counts at most 30 credits; until-cancelled is unchanged.
- **Web:**
  - Donate gains "For how long: Until I cancel / A number of times" whenever "How often" is not Once, with a number field. The total updates as you type: "3 × 1,000,000 = 3,000,000 adj. tokens over 3 days". The default stays "until I cancel".
  - The source card (Tokens & sources) and the Bank inputs table show "2 of 3 credits left, next on 2026-11-02", or "all 3 credits made" once done.
  - The mock server has a 3-credit trial key, and `test/donateTimes.test.ts` is new.
- **Docs:** docs/architecture.md (Town Bank paragraph) and docs/log.md are updated.
- **Mock-server picture:** form text read back by `~/shots/donate-times.mjs`: "For how long / A number of times / Times (the first credit is now) 3 / 3 × 1,000,000 = 3,000,000 adj. tokens over 3 days". The same script runs against live, signed in through a mocked /api/me and with every non-GET aborted, so nothing is posted: `node ~/shots/donate-times.mjs https://muster.town/workshop/`.
- **Plan for the continuation:** if CI is green, check the highest migration number on main again and renumber 074 if it is taken. Then merge and redeploy, run the live picture script, and rewrite [dc_pnarp2er0m](../../wiki/2026-10/2026-10-31-donate-spend-limit-line-for-pasted-api-keys-arp2er0m.md) (Donate) and [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md) (dailyInflow rule, `/sources` new fields `creditsTotal`, `creditsLeft`, `nextCreditAt`).
- **For the rollup:** this changes Bank code (credits and inflow). Mitchell asked for it in the 1:1, so its "Your call" line should name it.

## What I need from you
Nothing needed.
