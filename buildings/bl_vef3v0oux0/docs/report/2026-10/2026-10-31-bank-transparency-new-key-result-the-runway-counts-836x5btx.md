---
id: "dc_ah836x5btx"
type: "report"
state: "building"
title: "Bank Transparency: new key result, the runway counts what comes in (the Bank says \"0 days\" while 10M/day beats an 8.5M/day burn); proposal in your in-tray"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_08dd8xgkxy"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:59:07.476Z"
sessionId: "se_saohjmczmm"
createdAt: "2026-10-31T20:47:53.609Z"
updatedAt: "2026-10-31T20:59:07.476Z"
---
Live a986c47. Nothing of ours newly live since the last rollup (PR #188, merge 88cce35, is on main and not yet deployed); this rollup goes out early because a key result was written.

## Shipped
Nothing new live from this building since the last rollup. The "Not funded" split by building (PR #188, 88cce35) is merged and waits for the deploy; its note copy (step 2) is queued behind it (as_watgqqpzny).

## Decided
- [dc_08dd8xgkxy](2026-10-31-explore-the-bank-s-runway-says-0-days-while-inflow-dd8xgkxy.md) → approve. Nell 1's exploration: the Bank Overview "Next 30 days" says "Tokens left last at that rate: 0 days" (floor of 4,769,023 left / 8,463,105 per day trailing burn) while the Balance table two rows up says "Expected inflow per day 10.0M". The runway has no inflow term (web BankFinance.tsx:30, core finance.ts:116-131), so it reads 0-1 days on almost every day. Findings [dc_ulbwe2sdyf](../../note/2026-10/2026-10-31-findings-the-bank-s-next-30-days-says-the-tokens-l-bwe2sdyf.md). New key result kr_9o07vhujfn; proposal gr_rdzg83m0al (160k, projection and display only, no ledger change) is in your in-tray.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_jksobb0bwo "Not funded" stops growing and its note explains itself | gr_wp2rg302qu | not-started (step 1 merged, step 2 queued behind deploy 88cce35) | 83,094 / 150,000 |
| kr_9o07vhujfn runway counts inflow (new today) | proposal open | not-started | 0 / 0 |
| kr_fydnpd8ok2 adjusted-token mix | none (your choice; directed schedule fires 2026-11-01 02:00Z) | not-started | 0 / 0 |

Today's spend by lane: exploration 57,126 tokens (free under the goal: 2,150,194); directed 1,003,736 tokens.

## Needs from Mitchell
- One question in words, for whenever you decide the runway plan: should the Bank also show a separate "left this week under the 70M weekly cap" line, or is folding the cap into "inflow per day" (10M/day, as today) enough?

_Already waiting in your in-tray: 1 proposal (gr_rdzg83m0al), 0 requests, 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_9o07vhujfn: "The Bank's "Next 30 days" runway counts what comes in: it shows burn, inflow and net per day, and says "covered by the daily inflow" instead of "0 days" when inflow exceeds burn" (how to check: Bank → Overview → Next 30 days, signed out: rows Burn / Coming in / Net per day and a runway that matches GET /api/finance projection (dailyInflow, netDailyBurn, runwayDays or covered); with live inflow 10M > burn 8.5M it reads "covered"; from [dc_ulbwe2sdyf](../../note/2026-10/2026-10-31-findings-the-bank-s-next-30-days-says-the-tokens-l-bwe2sdyf.md))
