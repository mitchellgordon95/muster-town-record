---
id: "dc_4exx02zf9g"
type: "report"
state: "building"
title: "The 277,170 overdrawn gap: 277,104 from Fable sessions drawn against raw-sized credits (exposed by the 037 conversion), plus 66 from a Workshop allocation"
authorId: "ag_t5p8jfp9fk"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "redirect"
decisionNote: "Show the overdrawn breakdown on the finance page (from dc_4exx02zf9g). Don't rewrite Bank rows: whether to correct the ≈52,659 misbooked by migration 037 is Mitchell's call and is in my rollup. Instead, make the 534,040 reviewable at a glance: extend GET /api/finance with an `overdrawnBreakdown` (durable overshoot, subscription credits drawn past size, debits on deleted credits, allocation overspent) that sums to `overdrawn`, and show it on muster.town/workshop/#/finance under the overdrawn figure with a one-line note that the subscription part is a pre-conversion Fable draw (raw-capped credits converted by migration 037). Read-only over existing ledgers, no schema or accounting change. Add tests that the components sum to overdrawn. Branch + draft PR; say the head commit in your report."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-28T00:04:56.916Z"
sessionId: "se_t3c12yfafm"
assignmentId: "as_zd9tq0u3o3"
costUsd: 1.5608067
tokens: 78040
turns: 37
createdAt: "2026-10-28T00:04:28.846Z"
updatedAt: "2026-10-28T00:04:56.916Z"
---
## What I did
- Re-pulled live `GET /api/finance`, `/api/bank` and `/api/allocations` at 2026-10-28 00:01 UTC. The figures haven't moved: overdrawn is 534,040, and the General pool's durable is −256,870.
- Read `core/src/finance.ts`, `bank.ts` (`drawTokens`, `poolAvailable`), and migrations 023, 034 and 037.
- Rebuilt each component of overdrawn from the ledgers and the event log (`session.ended` counters, `bank.credited`, `budget.exhausted`, `bank.converted`).
- Read-only: no PR.

## Findings
**`overdrawn` (finance.ts) adds up four things:**
- durable debits beyond durable credits
- each subscription credit's debits beyond that credit
- debits on deleted credits
- allocation spend beyond the allocation's size

| Component | adj. tokens | How I got it |
|---|---|---|
| Durable overshoot (General pool) | 256,870 | 1,923,537 durable debits − 1,666,667 API-key credit ([dc_myhlhsevgz](2026-10-27-general-pool-s-negative-durabletokens-256-870-is-o-hlhsevgz.md)) |
| Subscription credits drawn past their size | **277,104** | Subscription debits 19,369,928 (21,293,465 usedBank − 1,923,537 durable) minus what credits can cover, 19,092,824 (31,433,326 credited − 3,285,992 expired − 9,054,510 left) |
| Allocation overspent | **66** | `al_wsihhgeb4c` (Town Workshop, retired): size 1,666,667, spent 1,666,733 |
| **Total** | **534,040** | The gap is 277,104 + 66 = **277,170** |

**What the 277,104 is (inference from code and events; I couldn't read individual debit rows because no endpoint lists them):**
- Before 2026-10-27 00:00 the Bank capped debits in **raw** tokens, so each credit was drawn down to exactly its raw size.
- Migration 037 then converted the two sides differently:
  - **Credits** at Opus 30 raw per adj.
  - **Debits** from their own counters at **Opus weights for every row** (037 line 59: "Bank debits (Opus)", cacheRead 0.01).
- For the 34 Opus-only and backfilled sessions this nets to 0.
- From 2026-10-26 20:29 (when sessions started carrying counters) to the conversion, **Fable** (and a few Sonnet) sessions convert to far more than raw/30: about 17 raw per adj., not 30. So a fully drawn credit now shows debits above its size.
- The timeline fits that mechanism:
  - Credits were drawn out between 20:29 and the "Prod has run out of budget" event at 22:43. Sessions in that window carry an estimated **292,657** excess, against 277,104 observed (≈5% high). I can't pin the residual without debit rows.
  - Sessions from 23:31 to 00:00 add another 51,875 excess, but that falls on the 100M credit that later expired, so it only shrank `expired` and doesn't show as overdrawn.
  - No sessions with counters ended during the overshoot window (22:43 to 23:31), so the 256,870 durable debt is unaffected. My earlier claim that the conversion didn't cause the durable debt still holds.
- The 292,657 splits into two parts:
  - **≈52,659** is a misbooking: 037 weighed Fable cache reads at 0.01 instead of Fable's 0.005. This is a one-off historical error in migration 037; current code books new debits model-aware. Fixing it would mean rewriting old Bank rows, which is a Bank-accounting change for Mitchell, so I stopped there.
  - **≈239,998** is real: Fable costs more per raw token than the Opus 30:1 the credits were sized at, so the raw cap under-charged those sessions.

**Attribution (event-log estimate, 20:29–22:43 on 10-26):**
- **By building:** Onboarding (`bl_hzjw0z0zlz`) 108,401; Workshop 93,896; Prod (`bl_xvgnd1fvh6`) 90,359.
- **Manager sessions, no assignment or grant (≈205k):** mostly Fable sessions by Pix, Kelly and Cleo. One Pix facilitate session was −11,282.
- **Work sessions (≈87.5k):**
  - as_7sp1b4xegj (Cleo, Prod) 29,908
  - as_slensazjwm (Pix) 22,561
  - as_do562o45r2 (Kelly) 11,525
  - as_74lmibldf8 (Cleo) 9,607
  - as_p290jxl92v 5,223
  - as_v6ck0ewkg6 5,071
  - as_f6bfifiogd 3,608
- **The 66** belongs to the Workshop allocation `al_wsihhgeb4c`. It's probably the same conversion effect on allocation spend; I didn't verify that.

**For kr_q9oiu7a6ci:** the ledgers can't break spend down by assignment today.
- `bank_debits` and `usage` carry no sessionId or assignmentId.
- `grantId` is set only on member-funded debits.
- I could attribute the above only by joining event-log `session.ended` to `session.started` (which carries assignmentId and purpose).
- A spend-by-grant/assignment view needs either the sessions table as its source, or a sessionId on debits. Adding the column is a schema migration, so Mitchell first.
- About 70% of the overshoot came from manager sessions with no assignment. The breakdown needs a "manager / no assignment" row to sum to `used`.

## What I need from you
Decide whether to ask Mitchell to correct the ≈52,659 misbooked by migration 037, which is a Bank-accounting change. Or accept the 277,104 as historical and have the finance page label it "pre-conversion Fable draw".
