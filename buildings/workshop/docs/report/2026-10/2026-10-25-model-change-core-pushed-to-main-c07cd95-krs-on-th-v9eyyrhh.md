---
id: "dc_h2v9eyyrhh"
type: "report"
state: "building"
title: "Model change core pushed to main (c07cd95): KRs on the building goal, a grant names one KR, blocked state; parked for live check"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Parked continuation does the live check of c07cd95. Migration 032 and human-only KRs are fine. Once live: Root's UI assignment starts, the Workshop shows blocked and I draft the goal's key results for Mitchell."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T18:42:15.665Z"
sessionId: "se_8v2pat6cjb"
assignmentId: "as_6ggmieufpu"
costUsd: 4.246094400000001
tokens: 275171
turns: 71
createdAt: "2026-10-25T18:11:52.243Z"
updatedAt: "2026-10-25T18:42:15.665Z"
---
## What I did
I shipped the core side of Mitchell's model change (notes [dc_bo7xuobtbv](../../meeting-notes/2026-10/2026-10-25-1-1-mitchell-and-pix-notes-7xuobtbv.md), mt_593ps69z8y) straight to main as **c07cd95** and queued a redeploy. It covers the schema, migration, core, server API, MCP verbs, prompts, docs and tests. `npm run typecheck` is clean and `npm test` passes across all packages (529 tests). I also made small edits to the web code so it still compiles; the real UI is Root's.

Two deviations from the assignment:
- **Migration number:** it is **032**, not 031, because 031 is already taken by the 1:1 migration.
- **Who writes the goal:** goal key results are human-only (`building.manage` plus a human caller). I did not change who can edit the goal sentence itself, so an agent manager can still edit it.

## Findings
**The model as built:**
- **Key results live on the building goal.** Each has text, howToCheck and a status. The manager can set status up to `claimed`; only someone with `building.fund` can set or undo `met` or `missed`.
- **A grant names one key result (`keyResultId`).** It carries `objective`, `approach`, `stopCondition`, `askTokens` and an optional `testingPlan` of up to 5 lines (text + howToCheck, no status). A grant can't be proposed or funded without a key result.
- **Lanes:**
  - `grant` names a grant; its key result is implied and stored on the assignment.
  - `exploration` names a goal key result that has no funded grant, or a gap sentence.
  - `laneHold` is unchanged.
- **`checkpoint_grant`** now takes `{grantId, reportId?, status?, note?}` and sets the status of the grant's one key result.
- **Blocked state:** a goal-directed building with no key results and no funded grant shows `"blocked: no key results to work toward"`.
  - On entering that state, `buildings.blockedAt` is set and the manager agent gets one "Get human decisions" assignment at the front of its queue: draft key results and put them to Mitchell through a rollup or the 1:1.
  - It doesn't fire again while the building stays blocked. Leaving the blocked state clears it, and the next time the building becomes blocked the manager is woken again.
  - It is checked after every grant, key-result or settings change, and on every scheduler tick.
- **Migration 032:** each grant's old key results became its testing plan, in order. `keyResultId` starts null. Assignments that named an old key result keep its text as their `gap` (exploration) or drop it (grant). So gr_jqsqra0dlx keeps its 3 key results as its testing plan, and the Workshop will show blocked.

**API shape for Root** (full table in docs/goal-directed-budgets.md, section "Model change"):
- **`GET /api/buildings/:id`** adds `keyResults: (KeyResult & {grantId|null})[]`, where `grantId` is the live grant on that key result, and `blocked: string|null`. The board response adds the same two fields.
- **Key-result routes:**
  - `GET /api/buildings/:id/key-results` returns `{keyResults, blocked}`.
  - `POST` to the same path takes `{text, howToCheck}`; human with `building.manage` only.
  - `PATCH /api/key-results/:id` takes `{status?, note?, text?, howToCheck?}`.
  - `DELETE /api/key-results/:id` returns 409 while a grant names that key result.
- **Grants:**
  - `POST /api/buildings/:id/grants` takes `{keyResultId, objective, approach?, stopCondition, askTokens, testingPlan?, findingsDocIds?}`.
  - `decide` takes `testingPlan?` instead of `keyResults`.
  - `GrantView` = Grant + `keyResult: KeyResult|null` + `spentTokens`.
- **Town Hall in-tray** returns `{reports, grants, blocked: [{buildingId, name, reason, since}]}`. Blocked buildings are not counted in the badge.

**Expect after the deploy:** every goal-directed building with no key results becomes blocked and its manager gets one wake. That includes the Workshop (Pix), and probably buildings created since goal-directed became the default (62af00f), if they have a manager agent. That is the intended behaviour.

## What I need from you
Nothing needed. Once c07cd95 is live, Root can start the UI, and Mitchell's next step is to write the Workshop goal's key results; Pix will propose them.
