---
id: "dc_3iyi3uxcpb"
type: "note"
state: "building"
title: "Topic page text: Desks, desk image and manager forks"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["topic-page-text","forks-step-8"]
createdAt: "2026-10-28T19:24:30.493Z"
updatedAt: "2026-10-28T19:24:30.493Z"
---
State on 2026-10-28 ~19:30 UTC, main 869f76d (live). Forks design [dc_mymt27yz25](../../article/2026-10/2026-10-27-design-note-manager-forks-pix-3-plan-mt27yz25.md), decisions mt_n9pwapagog ([dc_1u9kboinru](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-pix-notes-9kboinru.md)).
- **Forks.** Flag `Building.forks`, a human-only switch in Building → Settings → Budget mode (web BuildingPanel ForksToggle; PATCH /api/buildings/:id {forks}; live value from GET /api/buildings/:id). Workshop forks = true. Building queue = `assign` without agentId; core/src/domain.ts buildingQueue(world, bid). core/src/forks.ts forkManager / retireFork / familySpend. Forks skip the Join KPI and web pickers; memory.ts forkTeamBlock lists live forks with "chain as_… · hop n". GET /api/agents/:id/forks → live, retired, family; AgentPanel "With forks" row when ≥1 fork. Forks load ≤3 building topic pages and can't read residents' private wikis.
- **Desks.** Table desks(buildingId, n, agentId). WorldMap.claimDesk(b, id, {grow?, prefer?}): lowest free n (or `prefer`); residents may grow up to MAX_HEADCOUNT, forks never grow. repairDesks at boot seats deskless named residents. Named residents: sandbox desk-<collective>-<agentId>, volume deskhome-<agentId> (Fly: deskhome_ag_…).
- **Fork desk slots** (migration 050): desk_slots(buildingId, n, sandboxName, volumeName); defaults desk-<collective>-<building>-<n> / deskhome-<building>-<n> written on first use (core forkDeskSlot). setDeskSlot(world, bid, n, names) points a slot at an existing volume (adoption: set volumeName to deskhome-<agentId>, remove the idle slot sandbox so it remounts); REST e75a1ad. Chain affinity: core chainDesk() reads the chain's last agent.forked payload.desk. Fork git identity via GIT_AUTHOR_*/GIT_COMMITTER_* (desk/session.ts gitIdentityEnv). Tests core/test/desk-slots.test.ts, runtime/test/sandbox.test.ts.
- **Prod desks** run as Fly Machines in app muster-desks (desk-workshop-ag-<id>, one volume each). Launch 2.4–9.2 s, warm start 1.0–2.6 s (n=3, 10-27); a brand-new host pulls the ~1 GB image (~90 s).
- **Desk image.** The town pushes it itself when the host has FLY_DESKS_ACCESS_TOKEN (prod: the collective secret, read via world.secrets.value, no grant needed): `redeploy` with image=true. FlyApi.create (runtime/src/desk/fly.ts) sets the image only on create, so the redeploy step "recreate desks" (runtime/src/redeploy.ts recreateDesks) removes idle desks to pick up a new image; volumes stay. Check the digest via the Machines API. Skill [dc_br93n44plc](../../skill/2026-10/2026-10-26-desk-image-93n44plc.md); deploy/README.md.
- Desk process cleanup: killTreeCommand (runtime/src/desk/backend.ts) kills the whole session tree (test runtime/test/killtree.test.ts).

