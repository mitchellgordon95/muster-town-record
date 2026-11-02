---
id: "dc_v7ejy1j5ri"
type: "flag"
state: "building"
title: "can we move the building schedule into its own tab in the building UI"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_v7ejy1j5ri (Workshop, (38,52)): \"can we move the building schedule into its own tab in the building UI, and get rid of the Members tab. we can manage buildings and managers as one package via the town hall.\" Two changes to the building panel in the web client (packages/web BuildingPanel), one PR:\n1. Schedule gets its own tab. Today the schedule section lives under Overview → Schedule. Make a top-level \"Schedule\" tab in the building panel holding that whole section (active schedules with next run and repeat, paused ones, edit/pause/cancel for the manager, the fire log if there is one), and remove it from Overview. The pixel-art schedule board on every building (furniture piece `schedule:<buildingId>`, click or E; see dc_mhz91klzjk) must open the new Schedule tab, not Overview; same for any other link that deep-links to the schedule section (planning side bar, docs). Update the mock fixture and any web test that targets the old location.\n2. Remove the Members tab (today: Manager + live Forks + roles, see dc_wlq1jvqldy). Managers are managed from the Town Hall planning panel's \"Managers\" tab; check that tab really shows each building's named manager and lets an admin change it, and if it does not, add the missing piece there rather than keeping Members. Live forks are still visible on the map and in the manager's team-lead prompt; if the roles list (permission pills) has no other home, say so in the report rather than inventing a new surface. Delete the Members panel code and its api helpers that become unused.\nNo schema migration, no Bank change. Merge the green PR to main, queue a redeploy (image=false), say which commit should be live, and park the live check with resumeWhen {deploy: <sha>}: live check = guest view of the Workshop panel shows tabs without Members and with Schedule listing sc_fh7wt82tmc; clicking the Workshop schedule board opens the Schedule tab; one cropped picture (≤300 px tall) uploaded. Rewrite topic page dc_jcyf86dpdp (web client panels) to match. Budget your turns: push and park rather than waiting for CI."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T17:04:33.029Z"
flagPos: {"x":38,"y":52}
pickedUpAt: "2026-10-30T17:04:08.040Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-10-30T17:04:00.245Z"
updatedAt: "2026-10-30T17:04:33.029Z"
---
can we move the building schedule into its own tab in the building UI

and get rid of the Members tab. we can manage buildings and managers as one package via the town hall
