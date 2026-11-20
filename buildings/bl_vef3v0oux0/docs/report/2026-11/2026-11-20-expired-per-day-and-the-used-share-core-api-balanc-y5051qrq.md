---
id: "dc_8uy5051qrq"
type: "report"
state: "building"
title: "Expired per day and the used share: core, API, Balance sentences in PR #537, parked to merge on green"
authorId: "ag_a9ab63ttff"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T02:24:20.431Z"
sessionId: "se_nn6gfc6zrc"
assignmentId: "as_uei524nqp4"
costUsd: 2.5745639
tokens: 128728
turns: 45
createdAt: "2026-11-20T02:24:20.425Z"
updatedAt: "2026-11-20T02:24:20.431Z"
---
## What I did
Built step 1 of gr_z13gmx54su in one PR: https://github.com/mitchellgordon95/muster-town/pull/537 (draft). It is parked to merge when green. Verified with typecheck, core tests (1104 ✓), web tests (455 ✓) and server rest.test (28 ✓). The `check --fast` run passed docs, deadcode and typecheck, and its test files all passed before my 500 s timeout cut it off. CI runs the full set. Topic page: [dc_vavmt8j3h9](../../wiki/2026-11/2026-11-20-incoming-credit-unused-gr-z13gmx54su-plan-and-stat-vmt8j3h9.md).

## Findings
- **Exact per-credit identity, no approximation.** New core `finance-utilization.ts` puts `utilization` {d7, d30, check} on GET /api/finance. It counts the subscription credits created in each window (today plus the N−1 full UTC days before it, the same windows as split). For each credit, used = min(drawn, tokens). The rest is expired if the credit is past expiresAt, otherwise left. So used + expired + left = credited, exactly.
  - `drawnPastSize`: draws past a credit's size. These are in overdrawn, not in used.
  - `durable`: API-key credits, kept outside the identity.
  - `check.dailyDiff`: credited + durable must equal the daily rows' credited over the same days.
  - The stop condition does not trigger: the identity is exact.
- **Daily `expired`.** It uses the same rule as /api/finance `expired` and sources `expiredTokens`, dated by each credit's expiresAt day. Credits that expired before the window go in `daily.expiredBefore`. `dailyCheck.expiredDiff` (inside ok) checks Σ rows + expiredBefore = expired.
- **check:finance gets new lines.** It checks daily expired against finance.expired, and each day against the sources' credits expiring that day. It checks the utilization check itself. Per window, it checks the parts, then credited and expired against the sources' credits created in the window, then credited + durable against the daily rows. Against the live server these lines fail with "server older than gr_z13gmx54su step 1" until #537 is live.
- **Web (BankDaily.tsx).** Under the chart, one sentence per window. The 7 d one reads: "Last 7 days: X subscription tokens came in; Y were used (p%), Z expired undrawn (q%) and W are still left until renewal." Below them are a ✓ line (used + expired + left = credited for both windows) and a note that subscription tokens don't roll over. Each day shows Expired on hover, in its aria-label and in a table column.
- **Web (BankFinance.tsx).** The Next 30 days net row now reads "N / day more comes in than is used; unused subscription tokens expire at renewal, they are not saved". "surplus" is gone from the code.
- **Other files.** Mock server (toy expired and utilization), core, web and server tests, a new section in docs/bank.md, and docs/log.d.
- **Inferred, not checked live.** The 7 d used share will read a little below the 16.7% that daily rows gave in [dc_kmqlcmbs5u](../../note/2026-11/2026-11-20-findings-most-subscription-credit-expires-undrawn-qlcmbs5u.md). That is because it counts only draws on the window's own credits. Step 2 will see the real number.

## What I need from you
Nothing needed.
