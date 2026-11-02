---
id: "dc_fvye9685e3"
type: "report"
state: "building"
title: "Bank sign is live: FREE reads minus the overdraft, in red (PR #262)"
authorId: "ag_lvv4e4nlje"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Clean verification: sign −2,481,213 in red matches /api/bank overdraftTokens at 18:04:43Z; picture mf_k0u118kz0e; overdraft rise explained (≈1.75M new grant claims 03:15–03:30Z). Flow card/legend not red is as PR #262 specified (sign only); no follow-up unless Mitchell asks. Picture goes into the next rollup."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T18:07:19.205Z"
sessionId: "se_hxft3vx8sf"
assignmentId: "as_kfhwg4x4fh"
costUsd: 2.0331999
tokens: 101660
turns: 54
createdAt: "2026-11-02T18:07:08.409Z"
updatedAt: "2026-11-02T18:07:19.205Z"
---
## What I did
I checked all five items on the live town, signed out, and took one picture of the sign. I worked out what grew the overdraft from the grant history and the event log. Then I rewrote topic page [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md).

## Findings
- **Live commit:** GET /api/health reports 92336d0e (started 18:02:14Z). Both 2b8ba6e (#262) and dcfffe01 (#261) are ancestors of it, so both are live.
- **Sign (signed out, muster.town/workshop/?guest, on the lawn beside the Bank):** FREE reads **−2,481,213 in red**. GET /api/bank `free.overdraftTokens` returned 2,481,213 (freeTokens 0) at 18:04:43Z, an exact match. The number changes minute by minute: it was −2,447,741 a minute earlier, and the API gave 2,103,121 at 18:02Z.
- **Flow card:** it reads "3.4M claimed · −2.5M free" and its legend reads "Free −2.5M", matching overdraft 2,548,497 at that moment. These two show the minus sign but **are not red**, because PR #262 only colours the sign. If the card should be red too, that is a small follow-up.
- **Picture:** ![Bank sign live: FREE reads −2,447,741 in red](/api/media/mf_k0u118kz0e.png) (/api/media/mf_k0u118kz0e.png, 400×140 px).
- **Why the overdraft rose from ≈712k (03:09Z) to 3,281,745 (03:38Z):** overdraft = funded grants' remaining + 200,000 reserve + 5,000 retainer − general tokens. About 1.75M of the rise was new claims in that half hour:
  - gr_4tf9hd64d5 funded 200,000 (03:15Z).
  - gr_yu6qw3j9x5 funded 500,000 (03:29:23Z).
  - gr_8i952perny funded 500,000 (03:29:37Z).
  - Mitchell raised two grants that were held at their 100% checkpoint: gr_ukrou4zjha from 250,000 to 500,000 (+≈249k left), and gr_mjr7nb438v from 300,000 to 600,000 (+≈296k left).

  There were no earmarks or reservations (both 0). The other ≈0.8M is probably session spend outside grants drawing down general tokens. Sessions that ended in the window used 2,478,259 adj. tokens, but I did not trace which of them were outside grants, so that part is inferred.
- **Also live:** /api/finance/spend now carries `grants`: 18,592,279 spent on 47 grants (25 done 9,820,316; 6 cut 2,593,904; 16 open 6,178,059; 12 over funding by 899,521; grantsCheck ok, diff 0).
- **Topic page [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md)** now states the live commit, the sign's number and picture, the overdraft breakdown, and that #261 is live.

## What I need from you
Nothing needed.
