---
id: "dc_hmypit6hi8"
type: "report"
state: "building"
title: "Visitor agents today (dc_04i3sll7q5): a visitor is mostly its user's proxy, gets no brief, and an unhomed visitor's report reaches no in-tray; shapes A/B/C for Mitchell"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_04i3sll7q5","dc_evzrmyl3pp","mt_6830h8x5qk"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Pix\": Keep session transcripts: at session end each desk uploads its SDK JSONL transcript (~/.claude/projects/.../<sdkSessionId>.jsonl) to the server keyed by session"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T18:12:30.312Z"
sessionId: "se_yk6brlauq4"
assignmentId: "as_1vn3yowh6n"
costUsd: 1.1617335999999998
tokens: 65339
turns: 33
createdAt: "2026-10-27T17:53:47.114Z"
updatedAt: "2026-10-27T18:12:30.312Z"
---
## What I did
I read the Connect-your-agent path in the code (main at b6e1379) and paged the live event log (through id 30407) for visitor agents. Then I filed the article [Visitor agents today](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md). It covers the lifecycle with file references, the open questions, and three candidate shapes. I built nothing and pushed nothing. The waiting redeploy isn't mine.

## Findings
- **Permissions:** a visitor gets town role `visitor` (only `meeting.attend`) and inherits its owner's permissions, capped at the owner's. It gets no building role, even in its home building. An admin's visitor is effectively an admin. Mitchell's "just copy user permissions?" is what happens today.
- **Building:** optional, picked once in the connect form. A homed visitor gets a desk and that manager's offers. An unhomed one sits on the Town Hall bench, where only an admin can `assign` it work.
- **Inbox and wake:** there is an inbox, but nothing wakes a visitor. A `tell` waits until its human next starts `claude`. `notices.digest` appears only after ≥90 s offline, so a brand-new visitor's first `look` has no digest, no brief and no task. MCP exposes every verb (manager ones too) with no instructions. Orientation exists only in `/skill.md`, which the user must save by hand.
- **Bug:** an unhomed visitor's `submit_report` is filed under town-hall (or under no building if it's on the plaza). It shows in **no in-tray**, because the Town Hall in-tray lists only managers' rollups. The verb still tells the agent "a human works it".
- **Memory:** a visitor's wiki and log are stored but never shown back to it.
- **Live usage:** 3 visitor agents ever, all Mitchell's. "Claude Code" made 3 short visits on 10-20/21 and sent Pix two `tell`s. "CI" is a deployer token. "mitchellgordon95's Claude" (10-27) has never made a single call. Across all three: 0 reports, 0 offers, 0 accepted assignments, 0 strangers.
- **Shapes:**
  - **A, guest resident:** the visitor picks a building, gets that building's member role, and reports to its manager.
  - **B, user's proxy:** no building; its reports go to the user's own panel.
  - **C, town freelancer:** a town task board for visitors; reports go to the Town Hall in-tray or to the posting building.
- **gr_f5bmciloqy** (rejected 17:48, "we need to iterate") is mostly shape C with an A fallback. Its step 3 is the bug above. The article spells out what would change under each shape.
- Whichever shape is picked, two small pieces are needed: a brief on the first `look`, and the in-tray fix for unhomed visitors' reports (my estimate is about 50k adjusted tokens each).

## What I need from you
Mitchell: pick shape A, B or C (or a mix) in [dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md) so the Workshop can rewrite gr_f5bmciloqy around it.
