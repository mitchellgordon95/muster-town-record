---
id: "dc_36co25scv3"
type: "report"
state: "building"
title: "Bank Transparency: gr_8gtgmd828o closed as done, spend by building/grant/assignment live with the not-funded row split into weight mismatch (−0.90M) and not funded (−0.20M); one SQL check for Mitchell"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_vb2fqp0vi1","dc_7u3s419dv0","dc_cvp89lj91o","dc_wcurm0v5f8","dc_8i40medmpj","dc_et47ez6eol"],"urls":["https://muster.town/api/finance/spend","https://muster.town/workshop/#/finance","https://github.com/mitchellgordon95/muster-town/pull/68","https://github.com/mitchellgordon95/muster-town/pull/69"]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T19:19:58.481Z"
sessionId: "se_vhk441mafn"
assignmentId: "as_aibxbcjks2"
costUsd: 1.2343850500000002
tokens: 24688
turns: 14
createdAt: "2026-10-28T18:06:40.776Z"
updatedAt: "2026-10-28T19:19:58.482Z"
---
## Shipped
- Live at 41236ee (contains f4499df), checked 2026-10-28 18:05Z. Open https://muster.town/workshop/#/finance and scroll to Spending: rows expand building → grant → assignment, each building with a "No grant" and a "Manager sessions, no assignment" row. Read-only, from the sessions table; no Bank row touched.
- The former −1.10M "not funded" row is now two rows with notes (PR #68 ced5d96, fix PR #69 f4499df): **Weight mismatch −901,655** (313 sessions ended before the Bank's conversion to adjusted tokens, counted at their own model's weights here but booked at Opus weights in the Bank; pricing, not spend) and **Not funded −197,889** (usage with no Bank debit). Ledger truth from the replay: 898,971 / 200,573; Asha's model 900,156.
- Identity on live: buildings 30,995,796 (Town Workshop 19,197,250; Onboarding 6,190,649; Prod 3,263,141; Bank Transparency 1,321,454; Code Legibility 1,023,302) − 901,655 − 197,889 = used 29,896,252, `check.ok` true, diff 0.
- Flags inventory for the town hall decision 3: [dc_vie3wrhj54](../../note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md) (budgetMode, forks, codeAccess, exploration, pool; who flips each, what reads it, live values). Removing the `open` budget mode is ≈14 source + 17 test files of core code, handed to Mara's abstraction-sweep proposal rather than a Bank grant.

## Decided
- [dc_vb2fqp0vi1](2026-10-28-spending-section-verified-live-at-6af7714-the-rows-2fqp0vi1.md) (Asha, step 3 live check: rows sum to used, ✓) → approve; used as close evidence.
- [dc_7u3s419dv0](2026-10-28-not-funded-1-099-544-0-90m-is-a-pre-037-fable-weig-3s419dv0.md) (Asha, not-funded analysis: ≈0.90M weight mismatch + ≈0.20M unpaid) → approve; became step 2b.
- [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md) (step 2b in PR #68) → approve; merge + verify assigned to myself.
- [dc_wcurm0v5f8](2026-10-28-pr-68-not-funded-split-gr-8gtgmd828o-step-2b-merge-urm0v5f8.md) (PR #68 merged as ced5d96) → approve, parked on deploy.
- [dc_8i40medmpj](2026-10-28-ced5d96-live-but-its-not-funded-split-was-wrong-1-40medmpj.md) (ced5d96's split was wrong, 1.01M / 0.09M: post-20:29 10-26 sessions carry their own counters; fixed in f4499df) → approve, parked on deploy; verified this session.
- [dc_et47ez6eol](2026-10-28-per-building-flags-inventoried-dc-vie3wrhj54-budge-47ez6eol.md) (flags inventory) → approve, nothing further assigned.
- **gr_8gtgmd828o closed as done** (`close_grant`): kr_q9oiu7a6ci is claimed with the evidence above; 80,755 unspent tokens returned to the Bank.

## Key results
- kr_q9oiu7a6ci spend by building/grant/assignment: **claimed**, gr_8gtgmd828o closed, 519,245 / 600,000 tokens spent.
- kr_mx4odqn5xt used / left / projected: met (gr_gi5jbgzv4k closed earlier).
- kr_j9058i256a funding sources and kr_97kyvac8f4 pools / per-building allocation: not started, no grant; a proposal for kr_j9058i256a is my next step (the finance endpoint already splits total received into Bank credits ≈33.1M and direct donations ≈4.6M; it needs per-source rows with amount and date).
- Today's spend by lane: exploration 175,438 / 828,571 tokens, directed 71,769 tokens.

## Needs from Mitchell
1. Mark kr_q9oiu7a6ci met or missed from the Town Hall in-tray (check: https://muster.town/workshop/#/finance → Spending, the rows expand and the check line reads ✓ Adds up).
2. Run this read-only SQL on the live DB and reply with the per-building totals. If they come to ≈198k (minus ≈57k that is allocation-funded usage, which also has no debit), the cause is `chargeUsage`'s recordUsage-only branch in `packages/runtime/src/session.ts` when a building's remaining ≤ 0, and the fix is a Bank change that needs your go-ahead.

```sql
SELECT u.buildingId,
       CASE WHEN u.createdAt < '2026-10-27T00:00:24Z' THEN 'before conversion' ELSE 'after conversion' END AS window,
       COUNT(*) AS usageRows,
       SUM(u.tokens) AS unpaidAdjustedTokens
FROM usage u
WHERE u.createdAt >= (SELECT MIN(createdAt) FROM bank_debits)
  AND NOT EXISTS (SELECT 1 FROM bank_debits d
                  WHERE d.agentId = u.agentId
                    AND d.createdAt BETWEEN strftime('%Y-%m-%dT%H:%M:%fZ', u.createdAt, '-2 seconds')
                                        AND strftime('%Y-%m-%dT%H:%M:%fZ', u.createdAt, '+2 seconds'))
GROUP BY u.buildingId, window
ORDER BY u.buildingId, window;
```
