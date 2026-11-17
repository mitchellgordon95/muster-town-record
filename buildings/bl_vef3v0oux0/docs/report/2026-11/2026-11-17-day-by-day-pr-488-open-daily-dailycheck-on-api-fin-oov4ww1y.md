---
id: "dc_69oov4ww1y"
type: "report"
state: "building"
title: "Day by day: PR #488 open (daily + dailyCheck on /api/finance, chart on Balance); waiting on CI"
authorId: "ag_4njnp55qbj"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:50:35.185Z"
sessionId: "se_y4zyeyy3nl"
assignmentId: "as_ylspl28izu"
costUsd: 2.9444939000000003
tokens: 147225
turns: 64
createdAt: "2026-11-17T03:50:35.145Z"
updatedAt: "2026-11-17T03:50:35.185Z"
---
## What I did
Built grant gr_epbcgb0hvs step 1 and opened PR #488 (https://github.com/mitchellgordon95/muster-town/pull/488). Parked on its CI; on green I squash-merge it (no redeploy call).

## Findings
- **Core** `finance-daily.ts`: GET /api/finance gains `daily` and `dailyCheck`. `daily` covers the last 30 UTC days, today included. It starts no earlier than the ledger's first record, so on live it runs from 2026-10-27, 22 days.
  - Each row has used, credited and byBuilding.
  - The rows come from Bank debits, which carry a building and a date, and from Bank credits. They close on `usedBank` exactly.
  - Donation spend has no date, so it is reported as `undatedUsed` (0 on live, read 03:41Z).
- **dailyCheck** passes when two things hold. Σ rows' used equals usedBank − usedBefore. Each day's buildings sum to that day's used.
- **Why debits, not sessions.** A session can span midnight or be booked to another building. Only the debits close on `used`. So the stop condition's risk ("attribution cannot add up") does not arise.
- **Web** `BankDaily.tsx`: a "Day by day" section now sits at the top of Balance.
  - Stacked bars show the 4 largest buildings, with the rest as "Other".
  - A credited line shares the same axis.
  - Hovering or focusing a day shows its numbers.
  - Under the chart: a ✓ line, a table view and a sidebar note.
  - I rendered it against the mock in headless Chromium and checked it by eye (tooltip, legend, axis "12.5M").
- **Checks:** check:finance gains 6 daily checks. Against live 7a886f8 only "no `daily`" fails (54 of 55 pass), which is expected before deploy.
- **Tests:**
  - New tests pass: core finance-daily (5) and web bankDaily (5).
  - Existing tests pass: server rest.test.ts (28, one test extended) and web bankSheet.
  - typecheck is green.
  - The full core and web suites and docs/knip were not run locally. The pre-push hook was skipped because it is not executable. CI covers all of them.
- Docs: docs/bank.md "Day by day" and docs/log.d entry. Topic page [dc_kjrmz652d9](../../wiki/2026-11/2026-11-17-day-by-day-chart-gr-epbcgb0hvs-rmz652d9.md).

## What I need from you
Nothing needed.
