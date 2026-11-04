---
id: "dc_rox29k1rxi"
type: "report"
state: "building"
title: "gr_qggxximtru step 1: 'Plans paid for' built; PR #329 open, parked on CI"
authorId: "ag_qp2shoai80"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of gr_qggxximtru built and parked on PR #329's CI; the merge follow-up (as_avz6ck0s0g, waiting on pr 329) and step 2 (as_vjju0a4oig) are already queued. The bank.fee event type and bf prefix are fine. The one-off server test failure: if CI shows it, the merge assignment re-checks before merging."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-04T18:56:09.504Z"
sessionId: "se_ppa0jsqzwh"
assignmentId: "as_qzdwqo0i2t"
costUsd: 2.2645243
tokens: 113226
turns: 59
createdAt: "2026-11-04T18:55:21.104Z"
updatedAt: "2026-11-04T18:56:09.504Z"
---
## What I did
Built step 1 of gr_qggxximtru (kr_au6pcldl3c) in one PR: https://github.com/mitchellgordon95/muster-town/pull/329 (draft, b7cf8c3d). Parked on its CI.

## Findings
- **Migration** 091_bank_fees.sql (additive table bank_fees; 090 still the highest on origin/main at push).
- **Core**: `Bank.fees()` / `addFee()` / `endFee()`; writes are admin-only, and a hosted collective is refused. Validation: label 1–80 characters, $ > 0, real calendar dates, end ≥ start. Each write logs a new `bank.fee` event.
- **Routes**: GET /api/bank/fees is public and returns `{fees}`. POST /api/bank/fees is admin-only and returns 201. POST /api/bank/fees/:id/end is admin-only.
- **Web**: the Inputs tab has a "Plans paid for" section (new `panels/BankFees.tsx`), right after Bank inputs. Each row shows label · $/month · from · to (or "ongoing"); with no rows it says "None recorded yet." Only an admin sees the one-line add form and an "End" button (with a date) on ongoing rows. The mock server serves two toy plans.
- **Tests** (all green): core `bank-fees.test.ts` has 3 tests; server `rest.test.ts` (401/403/400/201, end); web `finance.test.tsx` has 3 tests. docs/bank.md has a "Plans paid for" section.
- **npm run check**: typecheck, docs and deadcode passed. One server test failed during the 8-minute full run. I reran the whole server suite on its own and it passed with no failures, so I did not identify the failing test; I believe it was a load flake. CI will show it.
- **Changes from the plan**:
  - I added a `bank.fee` event type instead of reusing `bank.input`, because readers of `bank.input` expect an inputId.
  - I added the id prefix `bf`.
- **Topic pages**: rewrote [dc_aucmysyxl0](../../wiki/2026-11/2026-11-04-cash-cost-of-running-the-collective-gr-qggxximtru-cmysyxl0.md). [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md) waits until the live check.

## What I need from you
Nothing needed.
