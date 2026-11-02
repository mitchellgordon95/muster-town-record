---
id: "dc_dlq2rtvl46"
type: "report"
state: "building"
title: "Workshop rollup 8: Bank grant plan ready (the Bank counts raw tokens, ~30× over adjusted output; 7 unexpected out-of-tokens deaths in 7 days); blocked only on the Workshop key result"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_jwt2rmekwi"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T15:45:51.893Z"
sessionId: "se_wbpb679hcn"
createdAt: "2026-10-26T15:21:22.162Z"
updatedAt: "2026-10-26T15:45:51.893Z"
---
## Shipped
Nothing new live since rollup 7 (live commit 119bd70). Filed: [dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md), the Bank accuracy findings and grant plan.

## Decided
- [dc_jwt2rmekwi](2026-10-26-bank-grant-ready-to-propose-findings-dc-2uqmfdittg-t2rmekwi.md) (Pix, parked): approved. The findings are in and the grant is written out; the continuation resumes at 18:00Z and files it with `propose_grant` the moment the Workshop key result exists. Key numbers from the event log (597 ended sessions, 10-20 to 10-26):
  - The Bank's `tokens` = input + output + cache read + cache write, all raw.
  - Real SDK cost per 1M raw tokens: Opus 5.5 $0.56 to $0.70, Fable 5.1 $2.06, Haiku $0.15.
  - At $20 per 1M Opus output tokens, 1M raw = 28k to 35k adjusted output tokens: the Bank over-counts ~30× (Opus), ~24× (Fable). Your "output plus 2%" guess is the right order; the data says ~3%.
  - Baseline: 7 unexpected out-of-tokens events in the week to 10-26 (3 subscription-cap deaths 10-25 22:18Z, 4 budget.exhausted).
- Grant plan (ask 24M raw): keep the per-kind usage breakdown per session; define adjusted output tokens with list-price weights per model; convert ledger and UI to that unit; nightly drift check against SDK cost plus cap-death logging; "deaths last 7 days" counter and a hold when the day nears the learned cap. Stop: 7 days with zero unexpected deaths and drift within ±10%.
- Manager-wake fix stays parked (town-hall decision 2); it blocks nothing here.

## Key results
No funded grant. Workshop has no key result yet, so the building is blocked; gr_jqsqra0dlx (rejected) is superseded by the Bank plan. Exploration spend this session: ~0.95M raw tokens on the findings.

## Needs from Mitchell
1. Write the Workshop key result at Workshop → Settings → Key results, with the text you agreed in the town hall (decision 1 of [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md): the Bank counts adjusted output tokens, starting from a calibration ratio; unexpected out-of-tokens deaths drop to zero over a week). The 18:00Z continuation then proposes the grant for you to fund.
