---
id: "dc_stx4kn4dto"
type: "note"
state: "building"
title: "Topic page draft: Desk slots and desks.maxRunning"
authorId: "ag_8uq6fnjis4"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_5lu51ts5qf","dc_s9kzuy4pp1","dc_cqkpp1uvdx","dc_4pagnhypv5","dc_vxgg8r55ha"],"urls":[]}
tags: []
createdAt: "2026-10-29T03:49:49.467Z"
updatedAt: "2026-10-29T03:49:58.891Z"
---
New page. Facts verified 2026-10-27; the stored value has not been rechecked since.

- "Desk max" / "Session slots" is `desks.maxRunning`: how many work sessions may run at once on the host. Schema is `DesksConfig` in packages/schema/src/index.ts (~line 1594). The default has been 30 since 62527f0 (2026-10-27; it was 20). Patch schema `DesksPatch`: positive int, max 1000.
- It is stored in the db (meta key 'desks'), so the code default only applies to a town with no stored row. Prod stored 6 on 2026-10-27 (the legacy deploy/cutover.sh set 6). Only an admin raising it changes that; a deploy doesn't.
- To change it live: Planning → System → Session slots (admin), or `PUT /api/town/desks {"maxRunning":N}` (routes/town.ts ~208, returns {desks, slots}).
- Where to read it: the Workshop health at /workshop/api/health has `slots` {running, max}. Root /api/health doesn't. Since 667c72b the hub serves the root and the Workshop lives at /workshop/ (client bundle /workshop/assets/main-*.js).
- The monitor's `slots` metric (monitor.ts) uses the same `slots()`: yellow at ≥80% for 15 min, red when full with pending assignments (no waitFor) for 15 min.
- The value 6 came from the old OVH VPS stress test ([dc_vxgg8r55ha](2026-10-21-stress-test-how-many-desks-muster-prod-1-ovh-d2-8-gg8r55ha.md), "6 desks at once"). That box is gone. The Fly Machine's ceiling is on the "Stress test" topic page (kr_z9lcfnvt94); check it before raising maxRunning far.
- Decision trail: 1:1 Mitchell/Cleo [dc_4pagnhypv5](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-cleo-notes-agnhypv5.md) (default 30), help-text removal [dc_17rbepma1h](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-cleo-notes-rbepma1h.md). Verified live in [dc_cqkpp1uvdx](../../report/2026-10/2026-10-27-62527f0-is-live-on-muster-town-health-shows-d08fcf-kpp1uvdx.md).

Sources: [dc_5lu51ts5qf](../../report/2026-10/2026-10-27-desk-max-now-defaults-to-30-62527f0-on-main-prod-s-u51ts5qf.md), [dc_s9kzuy4pp1](../../report/2026-10/2026-10-27-the-session-slots-help-text-is-gone-from-main-and-kzuy4pp1.md), [dc_cqkpp1uvdx](../../report/2026-10/2026-10-27-62527f0-is-live-on-muster-town-health-shows-d08fcf-kpp1uvdx.md).
