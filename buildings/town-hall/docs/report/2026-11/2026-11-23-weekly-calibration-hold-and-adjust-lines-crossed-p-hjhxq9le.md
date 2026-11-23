---
id: "dc_92hjhxq9le"
type: "report"
state: "building"
title: "Weekly calibration: hold and adjust lines crossed, policy ask ak_k70v4l0as6 filed"
authorId: "ag_lywy3igvel"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "pending"
sessionId: "se_312h9tam4j"
assignmentId: "as_lm7jt8o3sy"
costUsd: 1.5862486000000002
tokens: 79312
turns: 7
createdAt: "2026-11-23T04:06:19.779Z"
updatedAt: "2026-11-23T04:06:19.779Z"
---
## What I did
Read the calibration data (computed 2026-11-23 04:05 UTC) and filed one policy ask, ak_k70v4l0as6, with branches Adopt / Keep as is. Applied nothing to the table.

## Findings
- Two lines crossed. Hold share: 24 of 38 grants closed in 14 days held at their gate before closing (63%, line 25%). Adjust asks: 22 for 40 grants funded in 14 days (0.55 per grant, line 0.5).
- No size line crossed. Spend over price, last 30 days: S 1.08× over 22 steps, M 0.90× over 49, L 0.51× over 3 (the S and L samples are under the 30-step minimum). Median 2 sessions per completed step over 74 steps. 5 grants now hold at a gate with 0 tokens, oldest 9.3 h.
- The town's computed proposal was a no-op ("Raise S from 50,000 to 50,000"), so the card carries the smallest change the data supports: price an S step at 55,000 tokens (matching its 1.08× spend). Recommendation on the card: Keep as is, since every size spends inside its band and the holds track steps that take two sessions, which the table does not price.
- Last week's ask ak_r31emiv274 ("Require every L step to be split in two", recommended Keep as is) was still undecided when this session started; the hold line has now been crossed two weeks running (69% then 63%).

## What I need from you
Decide ak_k70v4l0as6 in the decision queue (Adopt or Keep as is).
