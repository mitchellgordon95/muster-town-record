---
id: "dc_7pgm2j5xg8"
type: "report"
state: "building"
title: "Planner is the Town Hall manager; message composer, \"Message from …\" path and Haiku ask deleted: PR #167 merged (bb80175), parked on its deploy"
authorId: "ag_5utjjwlthm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #167 = bb80175 merged (Planner is the Town Hall manager in name only, migration 066; composer, \"Message from …\" path and Haiku ask deleted). Live check already waits on deploy bb80175 as as_0c8d52ppqv. Goes in rollup 35 (not before ~21:50Z)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T18:05:44.794Z"
sessionId: "se_1lxt3vxgu7"
assignmentId: "as_bdmnsjgsq7"
costUsd: 0.8031528
tokens: 40158
turns: 22
createdAt: "2026-10-31T18:05:29.696Z"
updatedAt: "2026-10-31T18:05:44.794Z"
---
## What I did
The previous session's staged diff had survived as an auto-stash on my desk (stash@{0}, based on 49fb455), so I recovered it instead of starting over. Typecheck passed, so I committed and pushed it right away (f54ce65). `npm run check` then failed one server test (verbs.test.ts still called the deleted /message route). I fixed that test and the full check passed: docs, deadcode, typecheck and all tests (core 225, server 225, runtime 182, web 189, desk 37). I merged **PR #167** → main **bb80175** and queued a redeploy.

## Findings
- **Planner = Town Hall manager (in name only).** `Reorgs.ensurePlanner` sets the Town Hall's `managerAgentId` to the Planner. Migration **066_planner_manages_town_hall.sql** is additive: it fills the field from the existing Planner only where it is still empty. Code that leaves the Town Hall out, so its in-tray stays the humans' and the Planner keeps `plannerBrief` (1:1s and reorgs only):
  - `managerAgentOf` (core domain.ts)
  - `syncManagerRoles` (entities.ts), so the Planner gets no manager role
  - `Permissions.managesABuilding`
  - `Grants.requireWriter`
  - runtime `wakeManager` (manage.ts:57, unchanged behaviour)

  A Town Hall 1:1 with no agentId now goes to the Planner. The Town Hall gets no building queue or forks because `managerAgentOf` returns nothing for it.
- **Deleted:**
  - POST /api/agents/:id/message and `Ops.messageAgent` (with `MessageAgentOptions`/`Result` and the "Message from …" assignment path)
  - POST /api/agents/:id/chat, runtime `chat.ts` and its prompt in core prompts.ts
  - the web `Composer` and the quick-question "ask" UI in AgentPanel.tsx, plus `api().message`/`chat`, the mock routes, the composer styles and `message-agent.test.ts`
  - the matching cases in forks, meetings-chat-scheduler, manager-gate, assignment-queue and visitors tests
  - docs updated: architecture, wakes, goals, waterfall, design, README
- **Planner's Talk tab after:** the activity timeline and tells, then the callout "Planner is Town Hall's manager, the planning agent. Talk in a 1:1 … → Talk to ★ Planner" (opens `openPlanner`). There is no Forks tab for it.
- **Town Hall panel after:** a "Talk to ★ Planner" button for admins and goal owners, and a "Manager: ★ Planner, the planning agent …" row. Town Hall settings has no Manager select.
- **Other agent panels:** no composer; only a Stop button when the agent is working and you can control it.
- **Kept:** agent `tell`, 1:1s, the wakes relay in core wakes.ts (not dead: tells carrying a human origin still relay), GET /api/agents/:id/thread (the Talk tab still shows tells), and the visitor inbox via the agent API.
- **Should be live:** bb80175 (PR https://github.com/mitchellgordon95/muster-town/pull/167). Parked on that deploy; the live check comes next.

## What I need from you
Nothing needed.
