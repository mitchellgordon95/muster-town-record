---
id: "dc_7z5g5t1wl9"
type: "report"
state: "building"
title: "Model, daily budget, max turns and code access are now set once for the whole collective at Town Hall → Settings (PR #158 merged 2968f42, redeploy queued)"
authorId: "ag_2wshknigbo"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: PR #158 (2968f42) collective defaults at Town Hall → Settings, building Settings down to Desks. Live check queued separately. The \"save once\" ask goes into rollup 34's Needs from Mitchell (admin decision, his own thin-layer ask)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:26:07.097Z"
sessionId: "se_q3sj5u8o7r"
assignmentId: "as_siu3ksjrhn"
costUsd: 3.8973310999999997
tokens: 194867
turns: 78
createdAt: "2026-10-31T05:25:56.911Z"
updatedAt: "2026-10-31T05:26:07.097Z"
---
## What I did
Mitchell now sets the model, cheap model, daily budget per agent, max turns and code access in one place: **Town Hall → Settings → Collective defaults** (admins only). Saving applies them to every building at once. A building's own Settings no longer has these five fields, and its Overview shows them as one read-only "Collective defaults" line. Desks are now the only per-building setting.

PR https://github.com/mitchellgordon95/muster-town/pull/158, merged as **2968f42**. CI passed. I queued a redeploy, so 2968f42 should be live next; I have not checked it live. No desk image rebuild is needed (nothing changed in the desk image or its env).

![Collective defaults form](/api/media/mf_ja6d069zpx.png)
(Mock render of the Town Hall Settings section with live-like values. The line at the bottom names the buildings a save would change.)

## Findings
- **Where the values live:** `Town.defaults` (schema `BuildingDefaults`) in the town meta row, seeded from collective.json's new `defaults` block. The Workshop's 120 turns and code access moved there. `PUT /api/town/defaults` (admin only) saves them and copies them into every lab; the Town Hall is not changed. `createBuilding` copies them into a new building. `CreateBuildingInput`/`UpdateBuildingInput` no longer accept the five fields. Old collective.json files that set them per building still work when seeding. The Building columns still hold the values in use, so the code that reads them doesn't change: the family cap (daily × desks), DESK_MAX_TURNS, and the `model` option on `assign`/`schedule` all behave as before.
- **Live DB on first boot:** the stored defaults start from the oldest lab (Workshop: opus-5-5 / haiku-5-5 / 120 turns / 1,666,667 tokens a day per agent / code access on). Nothing is copied into the buildings at boot, so no building changes until an admin saves. The labs differ today: daily per agent is 1,666,667 for Workshop, 1,333,333 for Onboarding, 1,000,000 for Prod, Bank Transparency and Code Legibility, and 350,000 for UI/UX; max turns is 120 for Workshop and 80 for the rest. **The first save sets all of them to the form's values.** The form lists which buildings would change before you save.
- **Why the Town Hall's Settings and not the planning desk's System tab:** under the thin-layer decision these are town-level settings, and the Town Hall is the building that stands for the collective. The System tab holds host operations (session slots, redeploy), not settings that shape how buildings work.
- **Tests:** new core/test/collective-defaults.test.ts (the API drops the fields; saving copies to labs only; createBuilding copies the defaults; collective.json seeding; first-boot backfill with no buildings changed). server/test/desk.test.ts covers the route: a non-admin gets 403, a PATCH with codeAccess is ignored, an empty body gets 400. web/test/planDesks.test.tsx covers the form: admin only, and it names the buildings that differ. `npm run check --fast` and CI pass. The first CI run failed only because the manual went over its word limit; I fixed the wording.
- I updated docs/manual.md, docs/architecture.md, README.md (collective.json `defaults`), docs/log.md and docs/invariants/bank.md (renamed a test). I rewrote the topic page [dc_b1xrk44eu4](../../wiki/2026-10/2026-10-28-desks-desk-image-and-manager-forks-xrk44eu4.md).

## What I need from you
Decide on one value per field and save it once at Town Hall → Settings → Collective defaults. Until you do, each building keeps its current daily budget and max turns.
