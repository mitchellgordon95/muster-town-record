---
id: "dc_118grvgbwi"
type: "report"
state: "building"
title: "Ledger cutoff: PR #476 open, deletes Bank records from before 2026-10-27 00:00Z with a note; waiting on CI"
authorId: "ag_ps1fbi386c"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The deletion is Mitchell's own decision (town hall mt_dm14dgejml decision 4, 18:08Z: delete the records from before correct accounting, with a note), so no further ask: PR #476 merges on green under the merge rules' live-data line, and the hourly off-site backup (packages/server/src/backup/worker.ts:35) keeps the pre-cutoff rows recoverable. The continuation as_ve28wq5zj3 already waits on the PR's checks: merge if green, no redeploy, then read cutoff.removed live, check:finance, picture of the note. Its report must state the cutoff date and the row counts removed (decision 4 asks for both) and name the last backup stamp before the deploy."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-16T18:28:18.619Z"
sessionId: "se_jbmy3gng0o"
assignmentId: "as_oo20g6yark"
costUsd: 3.7969629999999994
tokens: 189848
turns: 72
createdAt: "2026-11-16T18:27:35.231Z"
updatedAt: "2026-11-16T18:28:18.619Z"
---
## What I did
- Wrote PR https://github.com/mitchellgordon95/muster-town/pull/476 (draft). It adds migration 117, `cutoff` on /api/finance and /api/finance/spend, a note on the Bank page, docs/bank.md and a log.d entry.
- Tests: core/test/ledger-cutoff.test.ts (2/2) and web/test/finance.test.tsx (53/53). `check --fast` was green except one timing test in server/test/backup.test.ts. That test passes when run alone (27/27).
- The plan and the live baseline are on topic page [dc_4ac3pazrih](../../wiki/2026-11/2026-11-16-ledger-cutoff-deleting-pre-adjusted-bank-records-c3pazrih.md).

## Findings
- **Cutoff: 2026-10-27 00:00:24Z.** This is the `bank.converted` event from migration 037, read from live /api/finance/spend `convertedAt`. Before it the Bank counted raw tokens split by a fixed back-fill ratio (30 raw per adj. token on Opus, 24 on Fable), with no real cache reads, input or cache writes.
- **What it deletes from before the cutoff:**
  - usage rows, debits and ended sessions;
  - expired credits that no later debit draws on;
  - cancelled inputs left with nothing;
  - retired donations.
- **What it keeps so that `left` never moves:**
  - debits on unexpired credits;
  - durable credits and debits, unless removing them leaves the durable balance the same. On live it does: the one durable credit, 1,666,666, is already overdrawn.
- **Number of rows removed: not known yet.** The migration runs on deploy. It writes the counts to `meta.ledgerCutoff` and to one `bank.pruned` event, and the continuation reads them from live `/api/finance .cutoff.removed`. From the API I can expect 11 pre-cutoff inputs and the 4 retired donations from 10-20. Some of those inputs' credits overlap the cutoff and will stay. I have no way to count debits, usage rows or sessions before it runs.
- **Note on the Bank page.** "Where the ledger starts" appears in the Balance, Inputs and Spending sidebars. It gives:
  - the cutoff and the reason for it;
  - the rows removed and the tokens they held;
  - "Grants funded before step sizes existed show no step rows: their steps had no size to price."
- **Side effect:** grants and agents from before the cutoff keep their records, but spend counted from their sessions now starts at the cutoff. Spending's pre-conversion rows should drop to 0: weight mismatch (901,655, 313 sessions) and Not funded (195,957).
- **Baseline at 18:09:33Z:** used 172,275,430; expired 211,255,098; left 21,883,746; total 404,229,370; overdrawn 1,184,904.

## What I need from you
Nothing needed. The PR deletes live data (merge rules: flag it). Merge it only if you accept that; the continuation merges it on green.
