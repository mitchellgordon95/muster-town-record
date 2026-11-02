---
id: "dc_554i5zu34l"
type: "report"
state: "building"
title: "Prod rollup #11: desk max default is 30 and the stale memory help text is gone (62527f0, live in d08fcf9); prod still stores 6, so Mitchell sets Session slots to 30 (outbox dc_cwgw3ab2g5)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_5lu51ts5qf","dc_s9kzuy4pp1"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-27T22:34:10.717Z"
sessionId: "se_ign5a0294s"
createdAt: "2026-10-27T18:53:36.426Z"
updatedAt: "2026-10-27T22:34:10.717Z"
---
## Shipped
- **Desk max default 20 → 30 and the out-of-date "0.2 GB per session" help text removed** (both 1:1 decisions, mt_xl7pre2q0u and [dc_17rbepma1h](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-cleo-notes-rbepma1h.md)): commit 62527f0 by Dara, live on https://muster.town (health commit d08fcf9 contains it). Changed: schema default, Session slots panel, mock sim, architecture.md, plan-meter.md, deploy/README.md, desks test. Reports [dc_5lu51ts5qf](2026-10-27-desk-max-now-defaults-to-30-62527f0-on-main-prod-s-u51ts5qf.md), [dc_s9kzuy4pp1](2026-10-27-the-session-slots-help-text-is-gone-from-main-and-kzuy4pp1.md). Demo: Planning → System → Session slots no longer shows the memory sentence.
- Prod keeps its stored value: muster.town still runs at **6** (set by the old cutover.sh in the db's `desks` meta), because a stored value beats the code default.

## Blockers and needs from Mitchell
1. **Set Session slots to 30** at Planning → System (admin), or `PUT /api/town/desks {"maxRunning":30}`. One field, no restart. Outbox request [dc_cwgw3ab2g5](../../../../../town-hall/outbox/2026-10/2026-10-27-set-session-slots-to-30-in-planning-system-gw3ab2g5.md).
2. Still open from rollup #10: run the Claude Code backup prompt [dc_go7ux3qzjb](../../note/2026-10/2026-10-27-prompt-for-claude-code-create-the-backup-bucket-se-7ux3qzjb.md) (outbox [dc_1ul3s3mpue](../../../../../town-hall/outbox/2026-10/2026-10-27-run-the-claude-code-prompt-for-the-backup-bucket-k-l3s3mpue.md)); Dara takes step 5 when it reports.

## Borderline decisions
- Neither Dara nor I have the `town.redeploy` permission now (both refused today), so Prod deploys rely on CI's green-main redeploy. It worked for 62527f0. If that permission loss was unintended, it's a one-line Town Hall fix; otherwise no action.

## Key results
- kr_z9lcfnvt94 stress test: done ([dc_eldvky6svj](2026-10-27-prod-rollup-8-stress-grant-gr-wqnunw5yd8-final-che-dvky6svj.md)), you mark it met; gr_wqnunw5yd8 452,597 / 1,000,000, early close with surplus once the Workshop ships that.
- kr_giqd28iwcb backup: on-track, steps 1-2 live, 3-4 wait on your Claude Code run; gr_jkorz4f49a 247,551 / 1,000,000.
- kr_wm6mphmrjf token rotation: not started, no grant (gr_ph4kky6r99 rejected).
- Spend today by lane: exploration 0 / 828,571; directed 66,047 (desk max work).
