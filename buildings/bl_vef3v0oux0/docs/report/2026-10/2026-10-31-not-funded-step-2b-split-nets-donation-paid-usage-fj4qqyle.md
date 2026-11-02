---
id: "dc_opfj4qqyle"
type: "report"
state: "building"
title: "Not funded step 2b: split nets donation-paid usage, with a reason when it still differs (PR #208 open, parked on CI)"
authorId: "ag_0fn2rfvmjw"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Your merge continuation as_5v0rxiprvz already parks on {pr:208}, so no new assignment from this. I re-queued step 3 (live check + picture) to wait on that merge instead of on as_7peyu8d7y6. On part (2): notFunded is booked − used (a net of sessions vs Bank used, finance-spend.ts:249-251) and the split is a heuristic over undebited usage rows (notFundedUsage, :156-194); they are structurally different numbers, so the live reason line is the honest answer. kr_518ed152d2 (\"adds up exactly\") will be Mitchell's call at close."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T21:51:40.553Z"
sessionId: "se_9ipa5v5elj"
assignmentId: "as_7peyu8d7y6"
costUsd: 0.7890796000000001
tokens: 39454
turns: 15
createdAt: "2026-10-31T21:50:55.754Z"
updatedAt: "2026-10-31T21:51:40.553Z"
---
## What I did
- Opened **PR #208** as a draft: https://github.com/mitchellgordon95/muster-town/pull/208. It is on branch `agent/nell-1/not-funded-step-2b-of-3-core-read-only-m`. It is read-only: no ledger change, no debit change, no new tables.
- **Core change** (`finance-spend.ts`, `notFundedUsage`): each building's undebited usage rows are now reduced by what that building's allocations spent. This uses the allocations' counters, the linkage the assignment allowed.
  - A building whose rows come to 0 after this drops out of the split.
  - `notFundedAllocationPaid` is now the amount taken out, not an upper bound.
  - When the split still differs from notFunded, `notFundedSplitCheck` carries a one-line `reason` (`NOT_FUNDED_SPLIT_REASON`).
- **Web change** (`BankFinance.tsx`): when a `reason` is present, the note shows "The rows by building come to X and Not funded to Y. <reason>" as a plain line in place of the red "These differ" line. The donation line now says that part is left out of the rows by building.
- **Checks:** typecheck passed. Core tests pass (`finance-spend.test.ts`, 7/7), covering both the case where the split matches after netting and the case where it differs and carries the reason. Web tests pass (`finance.test.tsx`, 24/24). I ran only these two files, not the full suites.
- I stopped before merging because a redeploy was waiting on my session to end.
- I did not rewrite [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md) this session: nothing new is live yet.

## Findings
- **Expected live after merge (inferred, not yet verified live):**
  - Workshop's 4,269,596 is fully donation-paid (it equals its allocation spend), so it leaves the split.
  - Onboarding 535,569 + Prod 123,238 = **658,807** vs notFunded **195,957**, so `ok` stays false and the reason shows.
  - That inference assumes Onboarding and Prod have no allocation spend. The live `notFundedAllocationPaid` equalling Workshop's figure exactly suggests this.
- **Part (2), why 658,807 ≠ 195,957, is not proven.** The reason text says what the structure implies:
  - notFunded is a net total: sessions booked − everything paid. Any session paid more than it booked cancels part of it.
  - The per-row split counts each undebited usage row in full.
  - I did not find a per-row linkage that would make the two equal exactly. I found no allocation id on usage rows or debits in the inputs `townSpend` reads.
- **Next session (continuation on {pr:208}):**
  1. If CI is green: mark ready, merge, and let CI deploy.
  2. Verify signed out with GET /api/finance/spend: split, `notFundedAllocationPaid`, `notFundedSplitCheck.reason`.
  3. Rewrite [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md).
  4. Then step 3 (as_qik35m0gtu) can run.

## What I need from you
Nothing needed.
