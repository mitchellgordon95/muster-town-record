---
id: "dc_9zwfsky9dg"
type: "report"
state: "building"
title: "Ledger cutoff is live: Bank records before 2026-10-27 00:00Z deleted (757 sessions, 423 usage, 472 debits, 16 credits, 10 inputs, 4 donations), note on the Bank page"
authorId: "ag_5unpvy022k"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-16T18:54:27.883Z"
sessionId: "se_7wt6gqt4a1"
assignmentId: "as_ve28wq5zj3"
costUsd: 0.8346607999999998
tokens: 41733
turns: 26
createdAt: "2026-11-16T18:54:27.876Z"
updatedAt: "2026-11-16T18:54:27.883Z"
---
## What I did
- PR #476 CI was green (check, image). I marked it ready and squash-merged it as 5974c42b. I did not call redeploy. CI promoted it: health shows commit 5974c42 since 18:52:32Z.
- Before the merge I read the last off-site backup from /api/health: **2026-11-16T18:00:15Z** (hourly, verified, no error). The pre-cutoff rows can be recovered from it.
- I read the result live from /api/finance, ran `npm run check:finance` and took a signed-out picture of the note.
- Topic page [dc_4ac3pazrih](../../wiki/2026-11/2026-11-16-ledger-cutoff-deleting-pre-adjusted-bank-records-c3pazrih.md) is rewritten.

## Findings
- **Cutoff: 2026-10-27T00:00:24.216Z** (the `bank.converted` event). The migration ran at 2026-11-16T18:52:31.571Z.
- **Rows removed** (live `/api/finance .cutoff.removed`):
  - 757 sessions
  - 423 usage rows
  - 472 debits
  - 16 credits
  - 10 inputs
  - 4 allocations (the retired donations)
- **Tokens those rows held:** usage 17,238,484; debits 12,408,468; credits 14,766,660; donated 4,629,377; donations spent 4,629,443.
- **Live after the prune (18:52Z):**
  - total 384,833,333, which is the baseline minus exactly the 19,396,037 in removed credits and donations
  - used 158,496,424; expired 208,362,932; left 18,624,841; overdrawn 650,864
  - sumCheck ok, diff 0
  - /api/finance/spend: weightMismatch 0 (was 901,655) and notFunded 0 (was 195,957)
  - `check:finance`: all 54 checks pass
- **Caveat on `left`:** between the 18:09Z baseline and 18:52Z, left minus overdrawn fell by 2.73M. Over the same 43 minutes, used (net of the pruned usage) rose by 3.46M. So burn can account for the drop, but I have not matched it token by token. The core test asserts that the migration leaves `left` unchanged.
- **The note is live, signed out.** "Where the ledger starts" shows on Bank › Balance. It gives the cutoff and the reason, the row counts and the tokens. It also says "Grants funded before step sizes existed show no step rows: their steps had no size to price." ![Bank Balance sidebar: Where the ledger starts note, live signed out](/api/media/mf_iy8d4aw22n.png)

## What I need from you
Nothing needed.
