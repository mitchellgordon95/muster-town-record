---
id: "dc_ny0vjg2bbe"
type: "report"
state: "building"
title: "Exploration: restarts revive 1:1s the human already left; proposed gr_xoso5f3oot (50k)"
authorId: "ag_ff3gebme66"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. Findings dc_d8u037mibg, topic page dc_45x33zqqdf. gr_xoso5f3oot (50k, one S step: quiet clock and post-restart wake count only human lines) waits in the decision queue with its card. Nothing to queue: the fix is the grant's step."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-21T00:12:02.397Z"
sessionId: "se_y0718f0qjj"
assignmentId: "as_blux10eyca"
costUsd: 1.2947156000000002
tokens: 64736
turns: 24
createdAt: "2026-11-21T00:11:46.829Z"
updatedAt: "2026-11-21T00:12:02.397Z"
---
## What I did
Pulled 7 days of sessions for the Secretary and the 7 managers from /api/sessions, and the transcripts of every cut 1:1 from /api/meetings. Read redeploy.ts (drain), prod-watch.ts, manage.ts (wakeTalker, closeQuietOneOnOnes), runtime index.ts (postRestartNotices) and docs/meetings.md §6. Wrote findings [dc_d8u037mibg](../../note/2026-11/2026-11-21-findings-redeploys-cut-1-1s-the-human-already-left-u037mibg.md) and topic page [dc_45x33zqqdf](../../wiki/2026-11/2026-11-21-1-1s-and-restarts-gr-xoso5f3oot-x33zqqdf.md). Proposed gr_xoso5f3oot. No code changed.

## Findings
- **Count.** Since 11-14 00:10Z, 19 1:1 sessions were "cut by restart": Secretary 17, Juno 1, Pix 1, all in Mitchell's 1:1s. The cut sessions cost 983k adj tokens, but that is mostly real conversation.
- **The premise is mostly wrong.** 11 of the 19 resumes had no human line waiting, and none arrived while they ran: **241,703 adj tokens**. This group includes all 10 cuts on 11-19/20 that Mara reported ([dc_1qha5spcyd](../../../../bl_vd69s5a1nh/docs/note/2026-11/2026-11-21-findings-14-of-work-sessions-only-check-the-live-t-ha5spcyd.md)). In mt_q4n1iwkcsc Mitchell never spoke, yet it got six pairs of a Town notice and a "Back again / Nth restart, nothing new" line, 12 min apart, from 01:53 to 02:55Z. In mt_mjxwzdhhd7 his last line was at 18:48 and four "Back" lines followed. The 8 resumes that did carry live human lines were on 11-15/16/17 (752k adj). How much of that the reload caused is not measured.
- **Mechanism.** The drain waits on a meeting session only 2 min (redeploy.ts:396-423). Prod-watch then restarts at most every 10 min, so merge runs restart the server about every 12 min. With no live session, any open 1:1 starts a fresh manage session that rebuilds the whole prompt (manage.ts wakeTalker, core oneOnOnePrompt). 1:1s never use SDK resume. postRestartNotices posts "reply is waiting" into every discussing meeting. The cause of the loop is closeQuietOneOnOnes (manage.ts:268-281): it counts every line and every session's start, so restarts keep an abandoned 1:1 open until the merge run ends.
- **Options.**
  - A. The quiet clock and the post-restart wake count only human lines, and the notice goes only where a human line is unanswered. One S step, about 240k adj a week saved (±50%). This option is proposed.
  - B. A longer drain while a human spoke recently. It saves an unmeasured part of the live resumes and delays deploys.
  - C. Skip the pull while a human 1:1 is live. Mitchell's 1:1s run for hours, so deploys stall.
  - D. SDK-resume 1:1s. Medium effort, unmeasured gain, and no help for idle 1:1s.
- **Proposed.** gr_xoso5f3oot "Stop restarts reviving abandoned 1:1s": 50,000 tokens, one S step, KRs kr_sf2tpl2lfg and kr_jb8qylny3t due 11-28, with a full ask card. Estimate line: 3 similar grants spent 147k–241k.

## What I need from you
Nothing needed. The proposal waits for a human in the decision queue.
