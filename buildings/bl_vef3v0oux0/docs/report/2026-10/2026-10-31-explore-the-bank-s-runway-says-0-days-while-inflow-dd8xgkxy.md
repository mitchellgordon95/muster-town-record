---
id: "dc_08dd8xgkxy"
type: "report"
state: "building"
title: "Explore: the Bank's runway says \"0 days\" while inflow (10.0M/day) beats burn (8.5M/day); proposed gr_rdzg83m0al"
authorId: "ag_uhvb4mjdbb"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_ulbwe2sdyf"],"urls":["https://muster.town/api/finance","https://muster.town/api/bank"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Checked against the snapshot: runwayDays (BankFinance.tsx:30) = floor(left / trailingDailyBurn), no inflow term; finance.ts projection has none either. Findings dc_ulbwe2sdyf sound. Proposal gr_rdzg83m0al waits on Mitchell in the Town Hall in-tray; nothing to queue until he decides."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T20:47:26.548Z"
sessionId: "se_6p8glhr3i0"
assignmentId: "as_ilveb3o54e"
costUsd: 0.6371072
tokens: 31855
turns: 15
createdAt: "2026-10-31T20:46:55.058Z"
updatedAt: "2026-10-31T20:47:26.548Z"
---
## What I did
Read live GET /api/finance, /api/bank, /api/health (2026-10-31 ~20:45Z, live a986c47) and the projection code (core finance.ts, bank.ts `dailyInflow`, web BankFinance.tsx `runwayDays`/`ProjectionView`). Wrote findings [dc_ulbwe2sdyf](../../note/2026-10/2026-10-31-findings-the-bank-s-next-30-days-says-the-tokens-l-bwe2sdyf.md), set key result kr_9o07vhujfn, proposed grant gr_rdzg83m0al (160k).

## Findings
- Bank → Overview → "Next 30 days" says **"Tokens left last at that rate: 0 days"**. It is floor(left 4,769,023 / trailing burn 8,463,105 per day) = 0.
- A few rows higher, the same page says "Expected inflow per day 10.0M". That is the active "Max plan" input: 15M/day, capped by its 70M weekly cap to 10M/day. Inflow beats burn by about 1.5M/day (approximate, since the burn is a 7-day average), so at this rate the town does not run out.
- The runway leaves out renewals by design (core finance.ts:116-131). It will read 0–1 days on almost any day, because what's left is mostly today's expiring credit. A stranger reads that as "the town is broke".
- The fix changes only the projection and how it's shown, with no change to the ledger. The projection gains dailyInflow, net per day and a runway that says "covered" when inflow ≥ burn. ProjectionView shows Burn / Coming in / Net / Lasts. Plan in three steps in gr_rdzg83m0al.
- Open question (in the findings): should there also be a separate "left this week under the weekly cap" line?

## What I need from you
Decide whether to fund gr_rdzg83m0al.
