---
id: "dc_8uptthmx6m"
type: "report"
state: "building"
title: "gr_ikgaundf5p (throwaway stop-test grant) funded: nothing to assign, fallback close scheduled for 11-06; its 5,000 tokens are already spent by this kickoff"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ihgbot3mq8","dc_goi17mocqe","dc_a1xvdmr2xe"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done as planned: nothing runs on the throwaway grant, the 11-06 fallback close sc_060f0dnpd2 covers the no-stop case, and a stop by Mitchell reaches me as a tell. The ask (stop gr_ikgaundf5p from the in-tray) goes into rollup 46's Needs; not an escalation, so no early rollup."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:01:49.427Z"
sessionId: "se_mrhjx0gigg"
assignmentId: "as_v1e1um45m3"
costUsd: 1.18879445
tokens: 59440
turns: 7
createdAt: "2026-11-04T18:01:28.531Z"
updatedAt: "2026-11-04T18:01:49.427Z"
---
## What I did
Read the plan: no work runs on this grant. It exists only for Mitchell to stop it from the Town Hall in-tray so the Workshop can read the Bank before and after a real stop (kr_una0o5bucs, due 2026-11-05). So I assigned no step. I put the plan's only other clause on the schedule: one-shot sc_060f0dnpd2 at 2026-11-06T12:00Z (lane grant, Haiku) that closes the grant as done if Mitchell has not stopped it by then, or reports the Bank numbers and the stopped row if he has. Wiki page dc_a1xvdmr2xe records the state.

## Findings
- The grant's test is weakened by the town's own paperwork cost: this kickoff session on Fable is charged to the grant and costs more than its 5,000 tokens, so spent will exceed granted and the "unspent rest" returned on a stop is 0. The Bank's free tokens will not rise. The rest of the check still works: the "Stopped: for the record" in-tray row with the reason, the deck slide, every key result missed with "Grant stopped: <reason>", the manager told.
- This is the same problem Pix 1 measured in [dc_goi17mocqe](2026-11-04-exploration-17-of-grant-spend-goes-to-two-fable-bo-i17mocqe.md) (kickoff + checkpoint = 17.3% of grant spend) and proposal gr_k69g04wwcg addresses. A future throwaway for the money check needs a grant large enough to survive its kickoff (50,000 or more), or that proposal funded first.
- Next rollup (46) should carry, under Needs from Mitchell: stop gr_ikgaundf5p from the in-tray with any reason (he funded it for that); the Workshop then reads GET /api/bank and pictures the row.

## What I need from you
Nothing needed (the ask to Mitchell goes in rollup 46).
