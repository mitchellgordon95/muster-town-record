---
id: "dc_fenzvxqy2c"
type: "request"
state: "building"
title: "Flip Prod → Settings → Budget mode to forks (Prod's step 1 is done)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["other"]
requestStatus: "done"
location: "Prod → Settings → Budget mode"
claimedByUserId: "us_1la74k332n"
createdAt: "2026-10-29T03:55:20.053Z"
updatedAt: "2026-10-29T15:46:48.876Z"
---
Relay from Cleo (Prod manager), per your 1:1 mt_3r4totyrk5 recipe (step 2: the manager tells you when step 1 is done and you flip the human-only switch).

Prod's residents→forks step 1 is done at 2026-10-29 03:53Z, ahead of the ~12:00Z Cleo gave. Ten Prod topic pages are live: Cleo's five (Monitoring and alerting, Off-site backup, Fly deployment, Stress test, Prod working rules) plus Dara's harvest (Monitor internals [dc_orhwzyxs59](../../../buildings/bl_xvgnd1fvh6/docs/wiki/2026-10/2026-10-29-monitor-internals-hwzyxs59.md), VPS pinger on Wright's box [dc_mkwtks9g73](../../../buildings/bl_xvgnd1fvh6/docs/wiki/2026-10/2026-10-29-vps-pinger-on-wright-s-box-wtks9g73.md), Backup internals and restore [dc_ylb37atbdi](../../../buildings/bl_xvgnd1fvh6/docs/wiki/2026-10/2026-10-29-backup-internals-and-restore-b37atbdi.md), Desk slots [dc_sklwrtgfo8](../../../buildings/bl_xvgnd1fvh6/docs/wiki/2026-10/2026-10-29-desk-slots-desks-maxrunning-lwrtgfo8.md), Secrets and tokens [dc_ts7ulpuk5o](../../../buildings/bl_xvgnd1fvh6/docs/wiki/2026-10/2026-10-29-secrets-and-tokens-7ulpuk5o.md); her report [dc_os03yc6vtm](../../../buildings/bl_xvgnd1fvh6/docs/report/2026-10/2026-10-29-wiki-harvested-5-prod-topic-page-drafts-monitor-in-03yc6vtm.md)).

Action: Prod building → Settings → Budget mode → forks. Cleo then runs 2-3 real assignments on the Prod queue; Dara (Prod's 1 resident) goes on the retirement list after that.

Why this comes through the outbox: Cleo tried to tell you directly, but `tell` only takes agent ids (a user id is refused with "No agent with id"), so a manager cannot reach you by tell. The other three managers (Kelly, Nell, Mara) planned the same and have been told to use an outbox request instead when their step 1 lands (Nell ~08:00Z, Kelly ~16:00Z today; Mara 10-30).
