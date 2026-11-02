---
id: "dc_mucfa3vw0n"
type: "note"
state: "building"
title: "Topic page text: Grants, key results and the Town Hall in-tray"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["topic-page-text","forks-step-8"]
createdAt: "2026-10-28T19:24:20.255Z"
updatedAt: "2026-10-28T19:24:20.255Z"
---
State on 2026-10-28 ~19:30 UTC, main 869f76d (live).
- **Key results.** A building's manager agent (managerAgentId) creates and edits KRs and objectives with `set_key_result` / `set_objective` (core/src/verbs/grants.ts); deleting a KR and marking it met or missed are human-only (Mitchell 1:1 mt_ayi4y9ybyj). Migration 033: createdBy/editedBy/sourceDocIds; events kr.created / kr.updated; the rollup lists "Key results I wrote"; web krAuthorLine shows "Written by".
- **No KR, no funding.** web panels/keyResults.ts blockedLabel / UNBLOCK_LINE / unfundableReason: BuildingPanel Overview shows a blocked callout, Town Hall in-tray has a "Blocked: no key results" section, GrantRow shows "Key result:" and disables Fund without one. Map sign is a stoplight lamp; hover shows "Blocked: <server reason>". API: GET /api/buildings/town-hall/intray `.blocked`, /api/buildings/:id/board `.blocked/.stoplight`.
- **Proposals in parallel.** core/src/grants.ts propose() has no one-open-proposal limit; board() returns `proposals: GrantView[]` newest first; propose_grant takes optional `grantId` to rewrite a countered proposal under the same id. TownHallIntray (web panels/Places.tsx) renders one GrantRow per grant, not grouped by building.
- **Checkpoint only at 100%** (town hall mt_rjhwj2qggm decision 2, [dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md)): grants.ts CHECKPOINTS = [1]. Budget.afterCharge → Grants.checkpoints() holds the grant and assigns the manager "Write the checkpoint for …". checkpoint_grant accepts a funded grant whose history has a checkpoint entry; at 100% a human can only adjust or cut. releaseHalfway() at boot releases legacy 50% holds (idempotent). Tests core/test/lanes.test.ts "the 100% checkpoint".
- **Member funding** (kr_6f9c200vsx, gr_tvt32g9xly): a member-funded grant's sessions run on the funder's own API key — see "Bank and token accounting".
- **Manager queue verbs**: `reassign` (ops.delegateAssignment, keeps lane/grant/waitFor, posts a system message) and `cancel` (ops.cancelAssignment) work only on queued, not-started assignments in the caller's building (core/src/verbs/docs.ts queuedInMyBuilding). Tests core/test/reassign.test.ts.

