---
id: "dc_reaxo5w9ni"
type: "report"
state: "building"
title: "Flag dc_v7ejy1j5ri merged (dcf7c1b, PR #113): Schedule tab, Members tab gone; live check parked on deploy"
authorId: "ag_ihr7ovetna"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_v7ejy1j5ri","dc_jcyf86dpdp","dc_mhz91klzjk"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/113"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. dcf7c1b (PR #113) merged, redeploy queued; the live check is already parked as as_fliquxk4oy on deploy dcf7c1b and starts itself. Goes into rollup 31 as Shipped \"Mitchell's flag: Schedule tab + Members tab gone\" once the live check lands; Your call: whether the planning desk Managers + Roles tabs are enough to manage buildings and managers as one package."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T17:12:46.750Z"
sessionId: "se_kby5011l3q"
assignmentId: "as_6cc3lzj97g"
costUsd: 1.4747896999999999
tokens: 73739
turns: 35
createdAt: "2026-10-30T17:12:38.976Z"
updatedAt: "2026-10-30T17:12:46.750Z"
---
## What I did
Implemented Mitchell's flag [dc_v7ejy1j5ri](../../flag/2026-10/2026-10-30-can-we-move-the-building-schedule-into-its-own-tab-ejy1j5ri.md) in one PR, https://github.com/mitchellgordon95/muster-town/pull/113. CI was green and I merged it to main as **dcf7c1b**, then queued a redeploy (image=false). **dcf7c1b should be live** after the restart. The live check is parked on that deploy. I rewrote topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) to match.

## Findings
- **Schedule tab:** a lab's building panel now has the tabs Overview | Goals | Grants | Schedule (Settings is added for managers). The Schedule tab holds the whole schedule list: next run, repeat, paused, last fired, what each run creates, and Pause/Resume/Cancel for holders of building.assign. It is no longer on Overview.
  - The schedule board on the map now opens the Schedule tab, and so does the red blocked badge's schedule link. The old scroll-to-section mechanism (`PanelRef.section`) is deleted.
  - The schedule board's hover text, docs/scheduling.md, docs/architecture.md and docs/log.md are updated.
- **Members tab removed** (the panel code and its CSS; there were no Members-only API helpers to delete).
  - The planning desk's Managers tab showed each building's manager but could not change it. I added a manager picker there for holders of building.manage. It lists the building's non-fork agents plus "none" and saves through the existing PATCH /api/buildings/:id. Clicking a manager now opens their agent panel.
  - **The roles list has a home:** the planning desk's Roles tab. That component moved from BuildingPanel into PlanningPanel. Building roles now show their building's name on the pill. Each role can be edited by holders of building.manage for its building, or of town.manage_roles.
  - docs/manual.md now tells members they are added at the planning desk → Roles.
  - Live forks are now shown only on the map and in the manager's team-lead prompt.
- **Checks:** typecheck is clean; all web tests pass (37 files, 147 tests). The new test web/test/buildingTabs.test.tsx checks the tab list and that the schedule appears on the Schedule tab and not on Overview. It also checks that the Managers tab names the manager.
  - **Not exercised:** a real signed-in "Set manager" save, since desks have no GitHub sign-in.
- There is no schema migration and no Bank change. The mock fixture needed no change.

## What I need from you
Nothing needed.
