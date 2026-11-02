---
id: "dc_hlw8qinzwh"
type: "report"
state: "building"
title: "Explore: \"Not funded\" stopped growing at 195,957; proposed gr_wp2rg302qu so its note explains the cause and the write-off"
authorId: "ag_qp334pfsrh"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_8qozlz0wsb","dc_cvp89lj91o","dc_i2ln43k253","dc_slumnj2s4z"],"urls":["https://muster.town/api/finance/spend"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Sound: notFunded flat at 195,957 since 10-29, cause pinned to pre-PR #131 chargeUsage, and the note half of kr_jksobb0bwo has no owner. gr_wp2rg302qu goes to Mitchell in the Town Hall in-tray on its own; write-off vs charge-back is his call there. Nothing to queue until he decides; sc_qu4lpdmgng keeps checking the number."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T19:54:47.703Z"
sessionId: "se_286bz5djwj"
assignmentId: "as_n67udlmxpf"
costUsd: 0.7347421999999999
tokens: 36737
turns: 13
createdAt: "2026-10-31T19:54:26.963Z"
updatedAt: "2026-10-31T19:54:47.703Z"
---
## What I did
I worked on one open key result, kr_jksobb0bwo (unpaid usage). I read the live spend endpoint, the old charging code before PR #131, and the earlier analysis. Findings are in [dc_8qozlz0wsb](../../note/2026-10/2026-10-31-findings-the-bank-s-not-funded-row-has-stopped-gro-ozlz0wsb.md), and I proposed one grant: gr_wp2rg302qu (150,000 tokens). I left kr_fydnpd8ok2 (adjusted-token mix) alone. Mitchell asked for that work as a scheduled job instead of a grant ("we're changing how grants work, maybe just schedule a cron", [dc_i2ln43k253](../../meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-nell-notes-ln43k253.md)), and that job, sc_p5oj6u7pks, fires at 2026-11-01 02:00Z. A grant for it would duplicate that job.

## Findings
- **The number has stopped growing.** Live `/api/finance/spend` at 2026-10-31 19:53Z (commit 49afcdd) shows notFunded = 195,957 adjusted tokens. It has been the same since 10-29.
- **The cause is confirmed in code.** Before PR #131 (b44a0b8, merged 10-31 00:36Z), `chargeUsage` (packages/runtime/src/session.ts:104–107 at b44a0b8^) skipped the Bank debit whenever a building had nothing left: it recorded the usage but charged nothing. Since PR #131, every session is charged as it runs.
- **The key result's second half has no owner.** It asks the note to say why the tokens went unpaid and whether they were charged back or written off. The live note (BankFinance.tsx:60) says neither, and the daily check sc_qu4lpdmgng only looks at the number.
- **What the grant does.** Step 1 computes a read-only split by building in the spend endpoint, using the rule from [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md); that split has never been run live. Step 2 rewrites the note with the cause, the date it stopped, the buildings, and "written off". Step 3 checks it live signed out. Write-off is the default because no Bank rows change. A charge-back would be a Bank change, so the work stops after step 1 if Mitchell wants that.

## What I need from you
Decide on gr_wp2rg302qu: funding it means the 195,957 tokens are written off; counter it if you want them charged back to the buildings.
