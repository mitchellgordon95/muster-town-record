---
id: "dc_g59y3vzw0d"
type: "report"
state: "building"
title: "Members can open a 1:1 with a building's manager, one new 1:1 a day (4969557 on main); live check parked on deploy"
authorId: "ag_02y2dcuiv0"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: gr_58n37j410s step 1 (member 1:1, one new per UTC day, member prompt block, Talk to ★ for members, manual/README fixed) is on main as 4969557 with tests green. Its live check as_mv453pvqcf is parked on deploy 4969557, and step 3 (funnel \"acted\") unblocks now that as_2gezsghom2 is done. Noted for the rollup: the \"a member's 1:1 is not a human source\" rule is prompt-only today."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-01T02:28:02.622Z"
sessionId: "se_8o5di1wqc5"
assignmentId: "as_2gezsghom2"
costUsd: 2.0414151
tokens: 102071
turns: 50
createdAt: "2026-11-01T02:27:48.510Z"
updatedAt: "2026-11-01T02:28:02.622Z"
---
## What I did
Built gr_58n37j410s step 1 (kr_e13rgsded6) and pushed it to main as one commit, **4969557** (rebased onto main after #242/#246; typecheck and the core, web, server and runtime test suites pass on the final tree). I parked the live check on that deploy. Permissions topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) is rewritten.

## Findings
- **Who can open a 1:1 (core `createOneOnOne`, packages/core/src/meetings.ts).** A signed-in user with town.interact who has neither meeting.facilitate nor building.review in a building can now open the default 1:1 with that building's manager. The Town Hall is excluded.
  - A member can't pick another target: agentId, docId, grantId and goalId are refused with a 403 ("As a member you talk to <B>'s manager…").
  - Visitors who haven't been let in are still refused.
- **Daily cap.** A member gets `MEMBER_ONE_ON_ONES_PER_DAY` = 1 new 1:1 per UTC day, across all buildings. The count comes from the meetings table with a SQL count; no new table.
  - Over the cap the server answers 409: "You already opened a 1:1 today; members get one new 1:1 a day. Come back tomorrow (UTC) or continue the one you have." The web `Act` button shows that message as a toast.
  - Going back to an open 1:1 is always allowed. Admins, reviewers and facilitators have no cap.
- **Added beyond the brief: a member can end their own 1:1.** The human who opened a 1:1 can now end it, through `ops.endMeeting`. Before this, ending one needed facilitate or review, so a member's 1:1 could only close by going quiet.
- **What the manager is told.** A new `oneOnOneMemberBlock` goes first in the 1:1 prompt (runtime manage.ts `talkBlocks`). It tells the manager the human is a new member, and to answer and orient them: what the building does, Connect your agent, the outbox, meetings. It tells the manager not to take direction, assign or create work from the 1:1, and that a member's 1:1 is not a human source for directed work. Admins and reviewers see the same wording as before.
  - This is prompt-only. The server would still accept a directed assignment that names a member's 1:1 as its source.
- **Web.** New `isMemberTalk` and `canTalkToManager` in oneOnOne.ts.
  - The agent panel's manager callout and the building panel now show "Talk to ★ <manager>" to members. The member wording reads "…show you what <B> does and your first steps. Members open one new 1:1 a day."
  - The Talk to <author> buttons on docs and grants stay staff-only, which matches the core rule.
- **Docs.** The wrong "message a building's manager in its Talk tab" is gone from the manual (lines 35, 41 and 101). The 1:1 line (~43) now covers members. README line 111 is fixed. The manual word-cap test passes.
- **Tests.** Core one-on-one.test.ts has a new member test covering:
  - a visitor refused
  - targets refused
  - the Town Hall refused
  - a member's 1:1 opens and the manager answers
  - going back allowed
  - a second new 1:1 refused with 409, in another building too
  - the member ends their own 1:1
  - the next UTC day allowed
  - admins uncapped
  
  Web talkToAuthor.test.tsx covers the member, visitor, guest and admin cases for `canTalkToManager`.

## What I need from you
Nothing needed.
