---
id: "dc_vv4slxqbmn"
type: "report"
state: "building"
title: "GET /api/finance built (draft PR #60): used, expired, left, overdrawn, a 30-day projection and a sum check"
authorId: "ag_t5p8jfp9fk"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Good work. Keep the identity used + expired + left = total + overdrawn and show overdrawn explicitly on the page (matches dc_myhlhsevgz). Merge of PR #60 goes to Mitchell in my rollup. Step 2 (as_8pqynhtvq4, Finance page) is queued for you: build it on top of the PR #60 branch so it doesn't wait on the merge; live verification of sumCheck happens in step 3 after the deploy."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-27T18:52:15.684Z"
sessionId: "se_964yd5jinl"
assignmentId: "as_ygdh70ot17"
costUsd: 1.1913633000000001
tokens: 64687
turns: 33
createdAt: "2026-10-27T18:50:25.469Z"
updatedAt: "2026-10-27T18:52:15.684Z"
---
## What I did
- Added a public, read-only `GET /api/finance`. The aggregation is a pure function, `financeSummary` in `packages/core/src/finance.ts`. It is wrapped as `world.bank.finance()` and the route is in `server/src/routes/town.ts`.
- Wrote 6 unit tests in `packages/core/test/finance.test.ts` and added a route assertion to `server/test/rest.test.ts`. I also documented the endpoint in `docs/architecture.md` and `docs/log.md`.
- Draft PR: https://github.com/mitchellgordon95/muster-town/pull/60 (commit `75ac1ea`). It is not merged, so I did not redeploy. The redeploy that is waiting now will not include this change.

## Findings
**What the endpoint returns.** All figures are in adjusted output tokens.
- `total = credited + donated`
  - `credited` is the sum of the BankCredit rows.
  - `donated` is the sum of the allocations. A retired allocation counts only what it spent, the same rule as `contributors`.
- `used = usedBank + usedDonations`
  - `usedBank` is every BankDebit, overshoot included.
  - `usedDonations` is the allocations' `spentTokens`.
- `expired`: for each expired subscription credit, its tokens minus what was debited from it.
- `left = leftBank + leftDonations`. It is never negative.
- `overdrawn`: durable debits beyond the durable credits, plus allocations spent beyond their size.
- `usageLedger`: the all-time sum of UsageEntry. It is informational only, because it can exceed `used`: usage with no funding source (e.g. the Town Hall, whose usage is never charged to a pool or allocation) is in the ledger but has no debit.
- `projection: {days: 30, trailingDailyBurn, burnDays, projectedUse30d}`. The burn is the usage ledger's last 7 days divided by `burnDays`. `burnDays` is 7, or the ledger's age in whole days (at least 1) while it is younger than a week.
- `sumCheck: {ok, diff, identity}`

**How I reconciled the overdrawn pool.** The sum check is `used + expired + left = total + overdrawn`, not the plain `used + expired + left = total` in the assignment.
- The overshoot debt (General pool durable −256,870, [dc_myhlhsevgz](2026-10-27-general-pool-s-negative-durabletokens-256-870-is-o-hlhsevgz.md)) is tokens that were really used but never received. With `left` held at 0 or above, the only way the identity can balance is if that debt appears explicitly as `overdrawn`.
- The identity holds exactly by construction:
  - Each expiring credit equals what was debited from it plus what expired or is still left.
  - The durable credits equal the durable debits plus durable left, minus overdrawn.
  - Each allocation equals what it spent plus what is left, minus any overspend.
  - A debit that points at a missing credit is also counted as overdrawn.
- So on live data I expect `sumCheck.ok` to be true and `overdrawn` to be about 256,870. I have not checked that yet; it needs the deploy.
- For step 2, the page can show "used X, of which Y overdrawn (overshoot debt)". If you'd rather drop the term, `used − overdrawn` gives a funded "used" that makes `used + expired + left = total` exact.

**Verification**
- `npm run typecheck` passes.
- `finance.test.ts`: 6/6 pass. It covers:
  - an empty town
  - a subscription credit part-debited and then expired (left 700 before expiry, expired 700 after)
  - live and retired donations
  - an overdrawn durable pool plus an overspent allocation (`overdrawn` 280, diff 0)
  - a projection with 2.5 days of history (averaged over 3 days) and with more than 7 days of history
  - an end-to-end case on a real Bank with an overshoot draw
- `bank.test.ts` and `budget.test.ts` pass.
- `rest.test.ts` passes, including the new `/api/finance` assertion, when run with `--testTimeout 60000`. At the default 5 s, two unrelated tests (different ones on different runs) timed out on this desk. Both pass with the longer timeout.

## What I need from you
Merge PR #60 and redeploy. Then `GET https://muster.town/api/finance` should show `sumCheck.ok: true`, which I'll verify next session.
