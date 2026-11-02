---
id: "dc_jwt2rmekwi"
type: "report"
state: "building"
title: "Bank grant ready to propose (findings dc_2uqmfdittg: the Bank over-counts ~30× vs adjusted output tokens; 7 unexpected out-of-tokens events in 7 days); no Workshop key result yet at 15:35Z, parked until 18:00Z"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_qg2gppz9jd","dc_2uqmfdittg","dc_lg8j3p38kl"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation resumes at 18:00Z and files the Bank grant once the Workshop key result exists. The KR ask goes to Mitchell in rollup 8."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T15:20:48.964Z"
sessionId: "se_ib1xekjb0d"
assignmentId: "as_xvaxwhm9ez"
costUsd: 3.3863797499999997
tokens: 31696
turns: 30
createdAt: "2026-10-26T15:20:18.771Z"
updatedAt: "2026-10-26T15:20:48.964Z"
---
## What I did
Checked the live Workshop (119bd70) for a key result after the town hall where Mitchell agreed its text: none yet (Prod and Onboarding have none either). So I prepared the grant so that `propose_grant` is a copy the moment the key result lands: read how the Bank counts tokens today, pulled the full event log (597 ended sessions) and computed the real cost per raw token by model, counted last week's out-of-tokens deaths, and filed the findings and the plan as [dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md). Parked until 18:00Z.

## Findings
- **The Bank counts raw tokens.** A session's `tokens` is input + output + cache read + cache creation, summed in `usageOf` and the breakdown discarded; every Bank number (inputs 40M+20M/day, allowances, grants) is in that unit.
- **Real cost per 1M raw tokens** (SDK cost, 10-20 to 10-26): Opus 5.5 $0.56 to $0.70, Fable 5.1 $2.06, Haiku $0.15. Per Opus session median $0.72, p10 $0.52, p90 $1.28.
- **Starting calibration ratio:** at $20 per 1M Opus output tokens, 1M raw tokens are worth 28k to 35k adjusted output tokens. The Bank over-counts about 30× for Opus and 24× for Fable. Mitchell's "output plus 2%" guess is the right order; the data says about 3%.
- **Baseline for the key result:** 7 unexpected out-of-tokens events in the last 7 days (3 subscription-cap deaths on 10-25 22:18Z, 4 `budget.exhausted`). What the claude.ai cap actually meters is unknown; step 4 of the plan learns it from where the cap hits.
- **Grant plan** ([dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md)): keep the per-kind breakdown per session (migration 031); define adjustedOutputTokens with list-price weights per model; convert the ledger and UI to that unit (Mitchell re-confirms the subscription inputs); nightly drift check against SDK cost plus cap-death logging; a "deaths last 7 days" counter and a hold when the day's spend nears the learned cap. Stop: 7 days with zero unexpected deaths and drift within ±10%. Ask 24M raw.
- **Manager-wake fix:** parked, as decision 2 allows. It doesn't block any Bank step. The held assignments on the rejected grant (Keel, Lena, Root) get re-assigned or cancelled when the Bank grant is funded.

## What I need from you
Mitchell: write the Workshop key result at Workshop → Settings → Key results (text in decision 1 of [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md)); the 18:00Z continuation then files the grant.
