---
id: "dc_tqa8u9i5ij"
type: "report"
state: "building"
title: "Model picker in the resident view pushed to main (12a1a89), redeploy queued"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:11:09.120Z"
sessionId: "se_b67ki9rcuk"
assignmentId: "as_y0hwhscydb"
costUsd: 0.7697389
tokens: 1562421
turns: 35
createdAt: "2026-10-21T04:06:48.905Z"
updatedAt: "2026-10-21T04:11:09.120Z"
---
## What I did
Added a model picker to the agent panel. It sits right under the permissions line. Pushed to main as 12a1a89 and called redeploy, so 12a1a89 should be live after this session ends.

## Findings
- **UI** (`packages/web/src/panels/AgentPanel.tsx`): a "Model" dropdown under the permissions. The choices are "Building default (<building's model>)", claude-fable-5-1, claude-opus-5-5, claude-sonnet-5-5 and claude-haiku-5-5. If an agent already has some other model set, that model is added to the list. When you save, a toast says the new model applies from the agent's next session. The map avatar resizes right away, because the agent update reaches the client over WS.
- **Who sees it:** the agent's owner, an admin, or a manager of its home building (building.manage). Humans, service agents and dismissed agents never get it.
- **API:** `PATCH /api/agents/:id/model {model: string|null}`, where null means the building default. The logic is in `ops.setAgentModel` / `ops.canSetModel`. Each change is logged as a system event. Work and meeting sessions already used `agent.model ?? building.model`, so nothing else had to change.
- **Verified:** typecheck is clean. Core tests 225/225 pass, including the new `test/agent-model.test.ts` (a manager can set and clear the model, a stranger is refused, a visitor's owner can set it). Server tests 61/61 and web tests 33/33 pass. In the mock UI I opened Noor's panel and picked Fable: the store's model and the dropdown both changed, the toast appeared, and there were no page errors.
- I haven't checked it on the live server yet; that waits for the redeploy.

## What I need from you
Nothing needed.
