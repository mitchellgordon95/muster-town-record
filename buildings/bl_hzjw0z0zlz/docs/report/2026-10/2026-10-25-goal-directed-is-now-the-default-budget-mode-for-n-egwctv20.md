---
id: "dc_d8egwctv20"
type: "report"
state: "building"
title: "Goal-directed is now the default Budget mode for new buildings (PR #52, e5dffd9): the default was open; schema default flipped, Town Hall stays open, existing buildings keep their stored setting; redeploy queued"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_eot3kv231u"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/52"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done as asked at the town hall (decision 4): PR #52 merged as e5dffd9, tests green, redeploy queued. Live verification goes to Craig once the deploy lands; result folds into the next rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-25T16:55:47.155Z"
sessionId: "se_of4zppd7ie"
assignmentId: "as_6pacj1qc9n"
costUsd: 2.5583810000000002
tokens: 41836
turns: 36
createdAt: "2026-10-25T16:55:03.126Z"
updatedAt: "2026-10-25T16:55:47.155Z"
---
## What I did
Checked the default from building settings (0059285): `Building.budgetMode` in `packages/schema/src/index.ts` defaulted to `open`, and `CreateBuildingInput` omits the field, so every new building got `open` from the Zod default. Changed it and merged: PR https://github.com/mitchellgordon95/agent-town/pull/52, merged to main as e5dffd9 (my commit 62af00f). Redeploy queued; e5dffd9 should be live after this session ends. Verified by `npm run typecheck` (green, all packages) and the core (253), runtime (116) and server (66) test suites, all passing.

## Findings
- **New buildings are goal-directed with the default exploration allowance.** The schema default is now `goal-directed`; `explorationTokensPerDay` keeps its default `null` (10% of the pool's daily inflow). A building made from the UI or API (`ops.createBuilding`) gets both; a new core test asserts it.
- **The Town Hall stays open.** `createBuilding` sets `open` for kind `town-hall` (no grants, zero exploration allowance), so a fresh install's Town Hall is not gated.
- **Existing buildings keep their setting, with no migration needed.** Migration 025 added the column `NOT NULL DEFAULT 'open'`, so every stored row already carries an explicit value; the table layer applies the Zod default only to missing or NULL columns. On muster.town the Onboarding, Prod, Carbon Cycle Lab and Town Hall stay `open`, the Town Workshop stays `goal-directed`; a human flips the others in Building settings.
- **Test fallout was small:** 3 of 253 core tests assumed the imported Carbon Cycle Lab was open (agents can create directed work only in an open building); they now set it open explicitly, and the lanes test sets the mode explicitly in both branches.
- Docs: `docs/goal-directed-budgets.md` rollout note and schema snippet updated, `docs/log.md` line added. The result goes into my next Onboarding rollup (this report lands in the Onboarding in-tray for me to decide and fold in).

## What I need from you
Nothing needed.
