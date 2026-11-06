---
id: "dc_xbiaxit5pr"
type: "report"
state: "building"
title: "Outbox rule noted; a Fly org token in the Town Hall secrets would let a Prod fork run the recovery drill itself (goes as the next rollup's Needs line); dc_6gnk7y16y1 is withdrawn once author-withdraw lands"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["mt_6kz0prkq8l","dc_ia2hybtuax","dc_6gnk7y16y1","dc_a3lvfa6vde","ms_sd50nk6lae"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Noted. The Fly-token question goes into the next rollup's Needs line (after the sc_ul1b1ntqik day-4 check at 05:20Z 11-06); dc_6gnk7y16y1 is withdrawn at the first team-lead session after Workshop's author-withdraw lands."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-05T20:02:45.972Z"
sessionId: "se_ocad7edmiy"
assignmentId: "as_xltnzoupp7"
costUsd: 2.44735105
tokens: 122368
turns: 18
createdAt: "2026-11-05T20:02:11.873Z"
updatedAt: "2026-11-05T20:02:45.972Z"
---
## What I did
Read Pix's relay of Mitchell's rule (mt_6kz0prkq8l, FYI [dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md)), the drill request [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md), deploy/recover.sh, docs/secrets.md and the stress-harness page, and checked this desk and origin/main. Replied to Pix (ms_0sspc2w0wn). Rewrote my Notes and the topic page "Recovery from a dead volume" ([dc_nh11dqbf19](../../wiki/2026-10/2026-10-31-recovery-from-a-dead-volume-11dqbf19.md)). No code, no outbox request, no rollup.

## Findings
- **Yes: a Fly token in the Town Hall secrets would let a fork run the drill.** Precedent: on 10-26 the stress throwaway was created, deployed from GitHub with deploy/fly/build.sh and destroyed from a Prod desk, using FLY_STRESS_TOKEN (an org token, a Town Hall secret granted to Prod) and the desk's GH_TOKEN. flyctl v0.4.122 is still at ~/.fly/bin on this desk.
- **What recover.sh needs:** an org token (it creates the app and a volume, deploys from `prod`, reads logs, ssh's into the throwaway, destroys it; an app-scoped deploy token cannot create or destroy the app), e.g. `fly tokens create org -o personal -n recover-drill -x 48h`, stored under a non-reserved name such as FLY_RECOVER_TOKEN (the fork exports it as FLY_API_TOKEN). Plus the five backup values (BUCKET_NAME, AWS_ENDPOINT_URL_S3, AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, MUSTER_TOWN_BACKUP_KEY) as Town Hall secrets; MUSTER_TOWN_ is a reserved prefix (packages/core/src/secrets.ts:15), so the key needs a name like RECOVER_BACKUP_KEY. The org token alone could read all five over `fly ssh console -a muster-town -C env`, but that touches the live app.
- **Trade-off for Mitchell:** an org token reaches muster-town for its lifetime, so a short expiry and a revoke afterwards (as with FLY_STRESS_TOKEN on 10-27). The throwaway boots with MUSTER_TOWN_RUNTIME=off: no sessions, no writes to the bucket. About 25 min and a few cents of Fly time, no restart of muster.town. On the desk it runs detached under nohup (the shell cap is 10 min); a cut session leaves `fly apps destroy recover-drill -y` for the next one.
- **Withdrawing [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md):** Workshop's author-withdraw (as_b784e3w2g5) is not on origin/main at 565a075, so it can't be withdrawn yet. It is on my Notes to withdraw at the first team-lead session after it lands. [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md) stays Mitchell's; [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) stays a real-world exception. Mitchell also deleted the old HOLD dc_y43rdv5zm7 at 19:48Z.
- **Next rollup** (after the sc_ul1b1ntqik day-4 check at 05:20Z) carries one Needs line: whether to put the Fly org token and the five backup values in the Town Hall secrets so Prod runs the drill itself. If he does, the drill becomes a grant-lane assignment on gr_z2v838adk9 instead of the 11-07 last-check schedule.

## What I need from you
Nothing needed.
