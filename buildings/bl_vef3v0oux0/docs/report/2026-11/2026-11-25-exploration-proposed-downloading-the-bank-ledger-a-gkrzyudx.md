---
id: "dc_c7gkrzyudx"
type: "report"
state: "building"
title: "Exploration: proposed downloading the Bank ledger as CSV (gr_igal9x7xnx)"
authorId: "ag_z8xpmi7014"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. gr_igal9x7xnx \"Download the Bank ledger as CSV\" (250k, M+S+S) is proposed with its card and waits for Mitchell in the decision queue; it has its own channel, so no separate ask. Findings dc_aihxf79h08 stand: the per-session rows tie out to the Bank's debits exactly on 11-23 and 11-24, and step 1 must measure the whole-ledger diff. Nothing queued."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-25T00:03:27.378Z"
sessionId: "se_kmrbb9a54v"
assignmentId: "as_8nlr13vxjz"
costUsd: 1.3176867000000003
tokens: 65884
turns: 31
createdAt: "2026-11-25T00:03:01.302Z"
updatedAt: "2026-11-25T00:03:27.378Z"
---
## What I did
I read the journal and the topic pages. Then I checked the three goals under ours against the code. Manager wakes and cost per decision, the cache-miss alert, spend by goal and grant sessions are all built already. I measured the live town at 2be107b4, wrote findings [dc_aihxf79h08](../../note/2026-11/2026-11-25-findings-nobody-outside-can-download-the-bank-s-le-hxf79h08.md) and proposed gr_igal9x7xnx under gl_5koas412u9. None of the journal lines covered this. The 2026-11-24 line ([dc_6wi0w2bh3w](2026-11-24-exploration-proposed-bank-headline-numbers-at-a-gl-i0w2bh3w.md), headline tiles) is the glance layer, and this proposal is the audit layer under it.

## Findings
- **The gap.** The Bank shows totals and its own ✓ checks, but nobody outside can re-add them. Nothing in the Bank exports its rows. GET /api/sessions caps at 200 rows and has no paging. On 2026-11-25 those 200 rows reach back only to 2026-11-22T18:30Z, while the last 7 days had 459 sessions.
- **The rows tie out to the Bank.** Per-session adjusted tokens summed by start day equal the Bank's debits exactly on two days:
  - 2026-11-23: 5,170,788 = 5,170,788
  - 2026-11-24: 3,889,619 = 3,889,619
- **Not checked yet:** history from before b44a0b8 (2026-10-31), and sessions that span midnight. Step 1 must measure the diff over the whole ledger and state it.
- **Live totals:** used 190,666,812, credited 559,833,333, expired 350,380,780, left 19,436,605 adj. tokens. The sum check passes.
- **Proposal gr_igal9x7xnx "Download the Bank ledger as CSV":** 250k (M + S + S), filed with its card. It adds two public files, one with every session and one with every credit, plus a `ledgerCheck` on /api/finance, links on the Balance tab, and a re-add in check:finance. Its key results are kr_d360yd1sqc, kr_h089bu9nmf and kr_wf0r2zllnm, all due 2026-11-29. The town's estimate: 3 similar grants spent 55k–288k.

## What I need from you
Fund or reject gr_igal9x7xnx in the decision queue.
