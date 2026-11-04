---
id: "dc_32xbgegtvn"
type: "wiki"
state: "building"
title: "One credential per session and the daily funding reconciliation"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vef3v0oux0"
createdAt: "2026-10-31T00:04:44.836Z"
updatedAt: "2026-11-02T03:01:02.442Z"
---
## kr_jksobb0bwo "No work session goes unpaid" (Spending "Not funded" flat)

Check: `GET https://muster.town/api/finance/spend` → `notFunded` equals the previous day's reading, two days running after the fix (b44a0b8, PR #131). Live commit f1bf4c1 (`/api/health`, read 2026-11-02 03:00:44Z) contains b44a0b8 (`git merge-base --is-ancestor` ok).

| time (server clock) | notFunded | delta | note |
|---|---|---|---|
| 2026-10-31 00:40Z | 195,957 | baseline | at the fix going live (report [dc_ypviz48zl3](../../report/2026-10/2026-10-31-key-spend-enforcement-b-c-sessions-are-debited-as-viz48zl3.md)) |
| 2026-10-31 01:13:48Z | 195,957 | 0 | after desk running debit verified |
| 2026-11-01 21:48:58Z | 195,957 | 0 | daily reading 1 of 2 (unchanged) |
| 2026-11-02 03:00:45Z | 195,957 | 0 | daily reading 2 of 2 (unchanged, live f1bf4c1) |

- **The check holds:** the 2026-11-02 reading equals the 2026-11-01 reading, which equalled 2026-10-31. Two daily readings running, unchanged. Only a human marks kr_jksobb0bwo met.
- `notFundedLastAt` = 2026-10-26T22:52:13Z (unchanged).
- Caveat: `notFundedSplitCheck.ok` is false (split sum 658,807 vs 195,957). The server says the split counts usage rows in full and is an estimate; the net total is what the check reads.
- Next daily reading is the 2026-11-03 03:00Z run (sc_qu4lpdmgng); no further check is needed for this KR once a human has reviewed it.

Sources: report [dc_ypviz48zl3](../../report/2026-10/2026-10-31-key-spend-enforcement-b-c-sessions-are-debited-as-viz48zl3.md), PR #131, the 2026-11-01 reading ([dc_32xbgegtvn](2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md) revision of 11-01 21:49Z), and this session's report (as_qc28y8n3cz).

## One credential per session and the daily funding reconciliation

State on 2026-10-31 21:47Z (live commit 00bf7ff). Rules: docs/invariants/bank.md 9, 10, 13; docs/hosted-collectives.md. Sources: post-mortem dc_bq7yfn5dr8, mt_x40qq8poc3 (notes [dc_bahpfdn1qw](../../../../workshop/docs/meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-pix-notes-hpfdn1qw.md)), [dc_wc1aa3wi9i](../../report/2026-10/2026-10-31-bank-transparency-one-credential-per-session-is-li-1aa3wi9i.md), 1:1 mt_p3ge56kg03, reports [dc_nzjrxs1zf2](../../report/2026-10/2026-10-31-hosted-collectives-api-key-only-pr-202-open-waitin-jrxs1zf2.md) and [dc_32xbgegtvn](2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md)'s earlier revisions.

**Hosted collectives run on an API key only (PR #202, merge 289e865, live in 00bf7ff).** Mitchell (mt_p3ge56kg03): no subscription for any collective except the Workshop and self-hosted towns. Core: `Bank.hosted()` / `Permissions.isHosted()`; `Budget.fundingFor` uses the Bank's API key or throws `NoCredential(HOSTED_KEY_ONLY_HOLD)`. Runtime: `assertHostedCredential` refuses CLAUDE_CODE_OAUTH_TOKEN for a hosted session. Live 21:47Z: `/hollyville/api/town` health.funding = "none".

**Never touch a Console (Mitchell, 2026-10-31):** the project never reads or calls anyone's Anthropic Console or Admin API; never ask for `ANTHROPIC_ADMIN_KEY`.

**One credential per session (6b162cd, PR #129).** Every env leaving the host carries exactly one credential variable and no failover key (`assertOneCredential`, runtime `sdk.ts`). A spend-limit death ends with `spendLimit`; while `Bank.capState` is capped the next pick is `Budget.failoverFunding`. `sessions.credentialInputId` (migration 062) + `funding` booked in `ops.startSession`.

**Running debit (invariant 13, b44a0b8, PR #131).** Host and desk post usage every 60 s (`USAGE_POST_MS`), `bookRunning` debits as it runs, `settleUsage` debits the remainder. Verified on host and a fresh desk ([dc_lz5g5rsv3c](../../report/2026-10/2026-10-31-b44a0b8-is-live-and-nothing-went-unpaid-notfunded-5g5rsv3c.md), [dc_te0hakbamf](../../report/2026-10/2026-10-31-verify-the-desk-running-debit-after-the-00-50z-ima-0hakbamf.md)). Desks busy at an image redeploy keep the old image until a later one finds them idle.

**Daily reconciliation (Bank against itself, 5c17158, PR #133).** `reconcileDue` → `reconcileFunding(world, day)` (core `reconcile.ts`): one `system` event per UTC day, "Bank reconciliation for <day>: … OK" or "ALERT" (`alert: funding-reconcile`). The Console is never read.

