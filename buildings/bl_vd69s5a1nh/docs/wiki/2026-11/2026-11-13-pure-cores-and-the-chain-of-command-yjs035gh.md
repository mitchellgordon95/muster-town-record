---
id: "dc_s4yjs035gh"
type: "wiki"
state: "building"
title: "Pure cores and the chain of command"
authorId: "ag_3bk3ltdc2z"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-11-13T06:20:59.477Z"
updatedAt: "2026-11-13T06:20:59.477Z"
---
Status 2026-11-13 (updatedAt is the stamp). Source: 1:1 mt_msnjkpgwdb decisions 13 and 15; assignment as_fts38a0zxd (Mara 2). Pix's old-rule PR #436 was closed unmerged; don't reuse it.

**PR #447 (draft, CI pending)**, branch agent/mara-2/chain-of-command-transform-as-a-pure-fun:
- `chainOfCommand({goals, buildings, rootId})` → Map buildingId → {answererGoalId, userId|null}; `answererOf(goalId, lookup, rootId)` for one goal. File packages/core/src/chain-of-command.ts. Rule: nearest captained goal at or above, else root. `Goals.ownerOf`, `route` and `tree()` call answererOf (one source of truth); a null root userId → shell uses firstAdminId.
- Property tests (fast-check, now a core devDependency): packages/core/test/chain-of-command.test.ts.
- One building per goal: `Goals.requireGoalFree` in createBuilding (POST /api/buildings, adopt, import), attach, retire's moveTo. Root and Town Hall exempt. Nesting legal. `Goals.nearestBuilding` / `buildingOn` replace entities.ts labOnChain and dead `buildingNear`. Adopt keeps refusing a lab above (visitor registers there instead).
- AGENTS.md standing rule 8: pure core + property tests.

**Still open from decision 15**: Bend 2 investigation (findings doc, ask Mitchell for his side project); reviewing jobs-grant PRs (answer(entry), ruleBlock, renderAsk) for the pure-core shape.

Live check after deploy: POST /api/buildings with goalId of a goal that has a building → 409. Live tree 2026-11-13 had no goal with two buildings.
