---
id: "dc_4ikvllnz7l"
type: "report"
state: "building"
title: "Grant proposed for Bank Transparency (gr_gi5jbgzv4k); waiting on a human decision"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_w2k9i2mkjy","dc_wjw5kittck","dc_8tkc3tar59"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal filed; waiting on the human decision on gr_gi5jbgzv4k. Asha already has queued exploration work. The next rollup will include this."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-27T06:31:11.924Z"
sessionId: "se_e35w2aqbdp"
assignmentId: "as_scvgo5m7vt"
costUsd: 0.1727842
tokens: 3746
turns: 5
createdAt: "2026-10-27T06:09:03.248Z"
updatedAt: "2026-10-27T06:31:11.924Z"
---
## What I did
I read Asha's finance data map ([dc_w2k9i2mkjy](2026-10-27-token-finance-data-map-for-the-four-bank-transpare-k9i2mkjy.md), approved) and proposed grant gr_gi5jbgzv4k. The building can only have one open proposal at a time, and that one is now in the Town Hall in-tray, so nothing else is left to do on this assignment.

## Findings
- The grant gr_gi5jbgzv4k is for kr_mx4odqn5xt (used / left / projected) and asks for 1.2M tokens. The plan: build GET /api/finance and a public finance page that show used, left and expired tokens plus a 30-day projection. The server checks that credited + donated = used + expired + left.
- Why this key result first: Asha's map shows the data for it is already recorded. It only needs aggregating and a page. The other key results need more groundwork:
  - kr_97kyvac8f4: buildings have no allocation amount, so it would have to use actual draws instead.
  - kr_q9oiu7a6ci: needs a join from session to building, plus an "unattributed" bucket for spend that can't be traced.
- Asha is working on as_cyvn58eym2 (exploration, kr_97kyvac8f4). On the live server, the General pool's durableTokens is −256,870, which is an anomaly she's checking.

## What I need from you
Fund, counter or reject gr_gi5jbgzv4k in the Town Hall in-tray.
