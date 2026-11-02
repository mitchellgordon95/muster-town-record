---
id: "dc_8o4mynsqqo"
type: "report"
state: "building"
title: "07f7957 live: an @mention with no human origin creates no assignment; the human-origin path still needs Mitchell"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_qua96t6vzp","dc_6h959oapbr","mt_pwcpdkmdyc"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Agent-side check done; the human-origin @mention test goes into rollup 17 Needs for Mitchell."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T05:50:43.990Z"
sessionId: "se_8z2cjjsllw"
assignmentId: "as_i6e5rmrqyb"
costUsd: 0.35013340000000004
tokens: 15506
turns: 12
createdAt: "2026-10-27T05:49:05.517Z"
updatedAt: "2026-10-27T05:50:43.990Z"
---
## What I did
I confirmed 07f7957 is live (/api/health commit 07f7957…). I read my session's origin from GET /api/agents/ag_wckat5qkk7/session, and it is `null`. Then I @mentioned Root, who was idle, in note [dc_6h959oapbr](../../note/2026-10/2026-10-27-wake-step-5-live-check-null-origin-mention-959oapbr.md) and checked the event log and Root's assignments. I changed no code. I ended early because a redeploy is waiting on this session, so nothing new needs to go live.

## Findings
- **Rule 3, null origin: passes live.** Event 27899 is `agent.mentioned` (toId Root, `origin: null`), and no `assignment.created` follows it. Root's only pending assignment is the earlier one about FLY_DESKS_ACCESS_TOKEN, which is unrelated. So the mention stayed inbox-only, as designed.
- **Rule 3, human origin: not checked live.** Desks have no human sign-in. The code path is covered by core test/wakes-step5.test.ts.
- Rules 1 (request_human answers) and 2 (amended decisions) also need a human action to fire, so they are not checked live either.

## What I need from you
Mitchell: sign in, write "@Root test" in a note or reply, and check that Root, who is idle, gets one "Mentioned by Mitchell: …" assignment. Mention again, and check that the second mention is added to the same assignment instead of creating a new one.
