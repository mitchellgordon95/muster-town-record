---
id: "dc_y9b9sy4rej"
type: "report"
state: "building"
title: "Desk image is live: desk Machines run sha256:7a7a79c8 and desk sessions post real five-counter tokens"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Desk image push verified live (sha256:7a7a79c8, real five-counter desk tokens). The FLY_DESKS_ACCESS_TOKEN grant removal is Mitchell's call; it goes in rollup 23 as a Needs line."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T19:09:17.176Z"
sessionId: "se_gf6bd8o00z"
assignmentId: "as_mxhofdobaf"
costUsd: 0.800986
tokens: 40049
turns: 25
createdAt: "2026-10-27T19:08:50.426Z"
updatedAt: "2026-10-27T19:09:17.176Z"
---
## What I did
After the restart (health f39c074) I read the redeploy events and listed the muster-desks Machines through the Fly Machines API using the desk token. I read the first desk `session.ended` after the restart and the Bank drift. I also rewrote the desk-image skill [dc_br93n44plc](../../skill/2026-10/2026-10-26-desk-image-93n44plc.md).

## Findings
- **Push events:** 31627 (18:53Z) "Redeploy: push desk image … ok". The drain then pulled 3 new commits, and event 31826 (19:06:36Z, step "push desk image (again)", ok, code 0) pushed "registry.fly.io/muster-desks:desk@sha256:7a7a79c82dd3cd7070806c8cf4cd0be8090290930ad6b93ff2a813cb45652f94". Event 31827, step "recreate desks", removed 14 desks (Pix, Root, Sage, Keel, Lena, Craig, Kelly, Dara, Cleo, Tae, Nell, Asha, Mara, Finn) and kept none.
- **Machines:** the 4 started desk Machines (Lena, Root, Tae, Keel) were all created at 19:06:58–59Z with `image_ref.digest` sha256:7a7a79c8…. The desk image label that went live is `registry.fly.io/muster-desks:desk` at that digest.
- **Sample session:** Lena se_v4ak0yhr5z (backend docker, started 19:07:02Z, event 31978):
  - input 2,838 / output 2,023 / cacheRead 189,506 / cacheWrite5m 0 / cacheWrite1h 20,850, with byModel present
  - booked 12,246 adjusted tokens against an SDK cost of $0.2449, a ratio of about 1.00
  - cacheWrite5m = 0 is normal for desks, which use the 1h cache. This is a real breakdown, not back-fill (`isBackfilled` is false because input and cw1h are non-zero).
  - Desk sessions before the push (e.g. 18:52Z) already had real counters.
- **Bank drift:** the last drift run covers 2026-10-26: Opus 0 sessions counted, 61 back-filled. Today's desk sessions have real counters, so they will count in the 00:00Z run for 2026-10-27. That can't be seen yet, and I can't trigger it (POST /api/bank/drift is admin-only).
- **Docs:** deploy/README.md and docs/secrets.md already describe the collective secret (from d3c779b). The skill [dc_br93n44plc](../../skill/2026-10/2026-10-26-desk-image-93n44plc.md) still said "host secret only, never reaches a desk". I rewrote it: it now covers the collective secret, the check through the Machines API, the "(again)" push, and why cacheWrite5m is 0.
- **Side note:** the server reads the secret with `secrets.value()`, which ignores grants. The image push therefore doesn't need the town-wide grant. Its only effect is to put a muster-desks deploy token (it can destroy Machines) in every desk's env.

## What I need from you
Decide whether to remove the town-wide grant of FLY_DESKS_ACCESS_TOKEN in Town Hall → Secrets. The push keeps working without it, and it stops the deploy token from reaching every desk.
