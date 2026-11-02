---
id: "dc_sex5q6p88g"
type: "report"
state: "building"
title: "Finance-page grant approved in the meeting but not funded yet; I'll assign the work once Fund is pressed"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["mt_6830h8x5qk","dc_4ikvllnz7l","dc_w2k9i2mkjy"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged. The building waits for Fund on gr_gi5jbgzv4k. That action is already on Mitchell's to-do list from mt_6830h8x5qk (decision 2). On the funded wake, assign Asha step 1 (GET /api/finance plus aggregation tests) in lane grant."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-27T17:44:13.333Z"
sessionId: "se_j3jiw4npd4"
assignmentId: "as_csio1v7sv9"
costUsd: 0.5338046000000001
tokens: 10904
turns: 10
createdAt: "2026-10-27T17:43:56.948Z"
updatedAt: "2026-10-27T17:44:13.333Z"
---
## What I did
I read the town hall record (mt_6830h8x5qk, decision 7) and checked the grant's live status at `GET /api/grants/gr_gi5jbgzv4k`.

## Findings
- In the meeting Mitchell said "fund" to gr_gi5jbgzv4k: the finance page for kr_mx4odqn5xt, a 1.2M-token ask. Live, the grant is still `status: proposed` with `fundedBy: null` and `spentTokens: 0`. Nobody has pressed Fund in the Town Hall in-tray yet. It is on Mitchell's to-do list (decision 2).
- Work can only run in the grant lane once the grant is funded, so I have not assigned it yet. Pressing Fund wakes me with a "Grant funded" assignment. Then I'll give Asha step 1: `GET /api/finance` with the aggregation that checks credited + donated = used + expired + left, plus unit tests for expiring credits and direct donations. The page and the 30-day projection follow.
- Noted for the next rollup: the new town-wide format has Shipped, Blockers/needs, Borderline decisions only, and a one-line key-result status, with no Decided section. No rollup is due now, because nothing was shipped or escalated since [dc_8tkc3tar59](2026-10-27-bank-transparency-rollup-four-key-results-set-gran-kc3tar59.md).

## What I need from you
Press Fund on gr_gi5jbgzv4k in the Town Hall in-tray.
