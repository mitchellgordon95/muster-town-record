---
id: "dc_tl9jkpn1j9"
type: "report"
state: "building"
title: "a5026c3 verified live: /api/bank shows 22 out-of-tokens deaths in the last 7 days and \"no cap seen\""
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Bank step 5 verified live on a5026c3: deaths counter 22 (10 cap + 12 exhausted) matches the hand count; no cap seen yet so the hold is dormant. The 7-day zero clock for kr_vyrhhiyotb starts now."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T00:36:28.993Z"
sessionId: "se_tzmp1wnr1l"
assignmentId: "as_rr10j43edh"
costUsd: 0.22801309999999997
tokens: 6709
turns: 6
createdAt: "2026-10-27T00:36:19.128Z"
updatedAt: "2026-10-27T00:36:28.993Z"
---
## What I did
Checked the live server: GET /api/health reports commit a5026c3 with accounting "adjusted". Then I read the `deaths` and `cap` fields from GET /api/bank.

## Findings
- **deaths** (rolling 7 days, since 2026-10-20T00:36Z): **total 22**, made up of 10 subscription-cap deaths ("org's monthly spend limit", each with a sessionId) and 12 budget.exhausted events. My pre-build count from the event log for 10-20..10-26 was also 10 cap + 12 exhausted, so the counter matches. The KR target is 0; the baseline in [dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md) was 7.
- **cap** (input bi_au5kt05vlj): `learnedCap: null`, `days: 0`. No bank.cap event has been recorded since step 4 went live, so the Bank page says "no cap seen" and there is no hold (`held: false`). Spent today is 380,015 adjusted tokens. A typical session (median of the last 50) is 21,510 adjusted tokens. The day resets at 2026-10-28T00:00Z.
- The hold has not run live yet. It will turn on only after the first bank.cap event teaches it a cap. Until then the tests in a5026c3 are the only check on it.
- Bank grant step 5 (as_23e58ae0lf) is done and live.

## What I need from you
Nothing needed.
