---
id: "dc_9ticra1d69"
type: "report"
state: "building"
title: "Planner 1:1 \"has no manager\": Mitchell's Stop at 17:37Z yesterday; fix in PR #236 (parked on CI)"
authorId: "ag_75xnk839gq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Cause confirmed (Mitchell's own Stop, event 72320 at 17:37:22Z 10-31; not a runtime bug). PR #236 is the right fix (ensurePlanner revives, 1:1 always targets the Planner, Resume for canPlan + visible on the Assignments tab, Stop/Resume record by). Its continuation as_82wl5dscgd (merge if green, redeploy, live-check the revive, add to dc_7lpbltjy1j) is already queued, so approve rather than continue. Mitchell told by tell ms_e4cp4dwj38 (Talk-tab Resume callout until #236 is live). Rollup 37 Shipped candidate once live-checked."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T01:22:32.230Z"
sessionId: "se_fp7emktbmf"
assignmentId: "as_1bpj8esg57"
costUsd: 1.2815685
tokens: 64078
turns: 17
createdAt: "2026-11-01T01:21:18.775Z"
updatedAt: "2026-11-01T01:22:32.230Z"
---
## What I did
I read the Planner's events on live, found the stop and fixed the 1:1 path and the missing Resume button. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/236. I tried to resume the Planner live; it failed (see Findings).

## Findings
- **Cause (event 72320, 2026-10-31T17:37:22.954Z):** "Planner was stopped". This text comes only from `Ops.stopAgent`, which the HTTP route POST /api/agents/:id/stop calls. The stop came 26 s into desk session se_0mqk1uafr3, which Mitchell's tell started (as_wiwjm93yyr). No agent tool call did it, and Mitchell confirmed in mt_d28u4ywau8 that he pressed Stop. It was not a runtime bug. The event did not record who pressed Stop; it does now (`payload.by`).
- **Why the 1:1 failed:** `planner()` still returns a stopped Planner. `oneOnOneTarget` then rejects it as not talkable, and `managerAgentOf` drops stopped agents too. So `createOneOnOne` threw "has no manager agent".
- **Why there was no Resume button:** an admin already passes `canControl` in the web. But for a stopped agent with an **empty queue** (the Planner's case), the Assignments tab only said "Stopped. Message the agent to start it again." with no button. Only the Talk tab had a Resume callout.
- **PR #236 changes:**
  - (1) `Reorgs.ensurePlanner` resumes a stopped Planner. The Town Hall 1:1 checks `canPlan` first, then always targets the Planner: by building, by the Planner's id, or "Plan with an agent".
  - (2) `Ops.resumeAgent` accepts anyone who `canPlan` (an admin or a goal's captain) for the Planner.
  - (3) Stop and Resume events record `payload.by`.
  - (4) Web: a shared `canControlAgent()`, and the Assignments tab shows Resume for a stopped agent with no queue. The web gate covers admins and Town Hall facilitators. Captains are allowed by the server, but the web store doesn't hold goal owners, so they don't see the button.
- **Tests:** new core `test/planner-stopped.test.ts` (3 tests). Typecheck passes; core 598, web 210 and server 250 tests pass.
- **Live resume:** I couldn't do it. POST /api/agents/ag_lywy3igvel/resume with the agent token returns 403 "building.assign". GET reads `status: "stopped"`. Mitchell can resume today from the Planner panel's Talk tab ("Planner is stopped. Resume"). Once #236 is live, just opening the 1:1 resumes the Planner.
- **Next session:** merge #236 if CI is green and redeploy. Then confirm the Planner reads idle, or that a Town Hall 1:1 opens rather than returning 409, and add a line to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).

## What I need from you
Nothing needed. Mitchell can click Resume on the Planner's Talk tab now if he wants to talk to it before the deploy.
