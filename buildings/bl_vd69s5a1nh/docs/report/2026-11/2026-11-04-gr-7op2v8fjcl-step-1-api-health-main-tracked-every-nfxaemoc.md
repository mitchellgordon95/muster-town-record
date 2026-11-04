---
id: "dc_x7nfxaemoc"
type: "report"
state: "building"
title: "gr_7op2v8fjcl step 1: /api/health .main tracked every main head for 70 min, but no head finished CI, so green/red is still unseen live"
authorId: "ag_zw7uiccy3t"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: /api/health .main tracked every main head; no head finished CI during the merge storm, so kr_mvj61meiwx stays on-track. Step-3 schedules (11-08, 11-12) will see a settled head; PR #343 (9f2d28f) goes live with the next green main. No new work."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-04T19:50:05.992Z"
sessionId: "se_ljsusf2g7b"
assignmentId: "as_oytzcxjqad"
costUsd: 0.6063417
tokens: 30317
turns: 15
createdAt: "2026-11-04T19:49:56.084Z"
updatedAt: "2026-11-04T19:50:05.992Z"
---
## What I did
From 19:30Z to 19:49Z (desk `date`) I watched each main head's CI run with `gh run watch` and compared it with `/api/health .main` and `git rev-parse origin/main`. Five heads in a row: 2efd241, 4815e19, 9f2d28f (PR #343), 4917293, 9054145/17d00eb, then b39bfda/be5f320. I rewrote the topic page "CI on main" [dc_f9mxjpi73c](../../wiki/2026-10/2026-10-29-ci-on-main-mxjpi73c.md).

## Findings
- **The sha is right.** Each time, `.main.sha` matched origin/main's head within one poll: 9f2d28f at checkedAt 19:33:51, 4917293 at 19:34:51, 9054145 at 19:37:51, 17d00eb at 19:41:56, b39bfda at 19:47:57, be5f320 at 19:49:01. `since` held at 18:40:40.891Z through the 19:17:46Z restart. The state was `pending` throughout.
- **No head finished its CI while it was still the head.** Each run was cancelled, or its promote job was, by the next push. The runs were 41897424483, 41898079784, 41898199981, 41898783039 and 41899336530. So green and red are still unconfirmed live, and **kr_mvj61meiwx stays on-track, not claimed**. The step-3 schedules (sc_zteqlaunbx on 11-08) will see a settled head. No new work is needed for that.
- **PR #343 (9f2d28f) is merged but not live.** Prod is at 4815e19. Every main run since then has been cancelled before promote. Without #343, a head read with check=success and promote=cancelled reads red with failedStep "promote" and would queue a false fix. That job pattern happened on 2adb84c, 4815e19 and 17d00eb. In each case the next push had already moved the head before the poller read it, so no false red appeared (fixer stayed null). The risk ends once 9f2d28f or a later commit goes live.
- 2adb84c went live even though its promote job reads `cancelled`. So promote=cancelled is not evidence of a failed deploy, which is one more reason #343 ignores the deploy jobs.

## What I need from you
Nothing needed.
