---
id: "dc_fhe4d6qgf3"
type: "report"
state: "building"
title: "gr_cuobjlny6r step 1: \"direct work under <goal>\" gate pushed to main as 92336d0e; live check parked on its deploy"
authorId: "ag_cwl8gltwp6"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: gr_cuobjlny6r step 1 (direct-work gate, migration 084, Let in + grant API, GET /api/members, /api/me direct) on main as 92336d0e; live check as_ek209s4uv5 parked on its deploy; step 2 as_wnv254c2ro unblocks now that as_pi5gjvlijz is done. Known: existing members lose Talk until step 2 lands (web still shows the button; 403 message on click). Folded into the 06:10 UTC rollup sc_w7vz73h9h2."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T03:49:55.286Z"
sessionId: "se_3yu4zh6xx7"
assignmentId: "as_pi5gjvlijz"
costUsd: 4.197624500000001
tokens: 209881
turns: 86
createdAt: "2026-11-02T03:49:35.002Z"
updatedAt: "2026-11-02T03:49:55.286Z"
---
## What I did
I built the core and server half of "direct work under <goal>" and pushed it straight to main as **92336d0e** (no PR, following the building's rule). The full `npm run check` passed before my final rebase: docs, deadcode, typecheck, and all core/server/web/runtime tests. After rebasing onto a busy main I re-ran typecheck, docs, deadcode and the affected tests, and they passed. CI on main was still running when I pushed. Twice under load, one test failed: `backup.test.ts` "runs in a worker thread… timers keep firing". It passes when run on its own, and my change doesn't touch it. I updated topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md).

## Findings
- **The gate:** I added `packages/core/src/direct.ts` `canDirect(world, who, buildingId)`. It is true when any of these holds:
  - the person can facilitate or review in that building;
  - they captain the building's attachment goal or a goal above it;
  - they are still a member and have a `direct_grants` row for one of those goals.

  Three places now use it:
  - **1:1s:** `createOneOnOne`. A member who isn't allowed now gets **403**, with a message containing "direct work under".
  - **Meetings:** `createMeeting` in labs.
  - **Directed work:** `lanes.ts` humanSource refuses a meeting or a tell as the source when none of its humans can direct work in the assigning building. A human's tell sent from their avatar now counts as a source; before, those were always refused.

  The plain-member branch and `oneOnOneMemberBlock` are deleted, so with no permission there is no 1:1.
- **Migration 084 `direct_grants`** (userId, goalId, grantedBy, createdAt). It is additive. Number 083 was taken by `083_grant_estimate.sql` while I was rebasing, so I renamed mine. The commit message body still says 083: it was already pushed and I didn't rewrite it.
- **API shape for step 2 (as_wnv254c2ro) and step 3:**
  - `POST /api/access-requests/:id/decide {grant, directGoalId?}` lets someone in and grants the goal in one call. The goal is checked before anything changes. Events: "@x was let in as a member" and "@x may direct work under "<goal>"".
  - `POST` and `DELETE /api/members/:userId/direct {goalId}` grant or revoke. They return `{direct}` and `{removed}`. Only an admin or a captain over that goal may call them; anyone else gets 403. Revoking logs "may no longer direct work under…".
  - `GET /api/members` is for admins or any captain. It returns `{members:[{userId,name,githubLogin,avatarUrl,letInAt,direct:[{goalId,text,grantedBy,createdAt}]}]}`.
  - `/api/me` now also returns `direct:[{goalId,text,how:"granted"|"captain"}]` and `directDefaultGoalId`: the decider's captained goal, else the town goal for an admin, else null.
- **Test:** `packages/server/test/access.test.ts` has 'direct work permission gates 1:1s, meetings and directed sources'. It covers:
  - Let in + grant in one call;
  - a plain Let in gets 403 on a 1:1 and on a meeting;
  - a holder inside the goal's subtree is allowed, and is refused in another lab;
  - a holder's first 1:1 line counts as `acted` once;
  - directed sources from a non-holder's tell or old 1:1 are refused;
  - a non-admin grant gets 403; an admin grant, then revoke.
- **Also changed:** the manual's member lines, README line 111 and docs/log.md are updated; the manual is at 1,848 of 1,900 words. Three existing tests were adjusted to the new rule: core one-on-one, join-funnel and lanes.
- **What a human checks once it's live:**
  - **kr_qtmcpalo80 (server half):** a let-in member without the grant gets 403 from POST /api/buildings/<id>/one-on-one.
  - **kr_t7rw103x6u (server half):** a holder's 1:1 is accepted as `sourceId` for directed work in that building.
  - **kr_3huiw2mea7:** CI is green on 92336d0e and the named test is present.
- **Behaviour change now live once deployed:** existing members lose Talk until someone grants them a goal. The web still shows Talk to them until step 2 lands; clicking it will get the 403 message.

## What I need from you
Nothing needed.
