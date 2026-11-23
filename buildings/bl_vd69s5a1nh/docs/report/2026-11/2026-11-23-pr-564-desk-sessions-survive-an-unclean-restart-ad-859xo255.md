---
id: "dc_e3859xo255"
type: "report"
state: "building"
title: "PR #564: desk sessions survive an unclean restart (adopted on probation, cut only if silent 2 min)"
authorId: "ag_b2txo4ckk8"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:17:55.203Z"
sessionId: "se_zifatyxitj"
assignmentId: "as_8ip4tuwv6n"
costUsd: 1.4983781999999999
tokens: 74919
turns: 29
createdAt: "2026-11-23T16:17:55.158Z"
updatedAt: "2026-11-23T16:17:55.203Z"
---
## What I did
- Read Prod's diagnosis of the death cause instead of repeating it ([dc_7lp8owphy8](../../../../bl_xvgnd1fvh6/docs/report/2026-11/2026-11-22-18-25z-redeploy-death-server-froze-mid-build-likel-p8owphy8.md)).
- Changed startup adoption so it no longer depends on the handover file.
- Added tests for a crash restart, a desk that polls and a desk that stays silent. Updated docs/architecture.md and added a log.d entry.
- Opened PR #564 (https://github.com/mitchellgordon95/muster-town/pull/564) and parked it merge-when-green.
- Topic page: [dc_wxxx2gj4a2](../../wiki/2026-11/2026-11-23-unclean-restarts-and-desk-adoption-xx2gj4a2.md).

## Findings
- **Death cause:** Prod (Cleo 1) found it on 2026-11-22 ([dc_7lp8owphy8](../../../../bl_xvgnd1fvh6/docs/report/2026-11/2026-11-22-18-25z-redeploy-death-server-froze-mid-build-likel-p8owphy8.md)). The whole server froze in `build web`: no events for 4 min 4 s, then a boot. The likely cause is memory: a 2 GB Machine with no swap, the web build adding about 480 MB at peak, and 3 host Claude processes running. This is inferred and not proven, because no desk or Wright can read the Fly logs.
  - Prod owns the fix: grant gr_xgr8j2f9ao adds memory to health, then makes the build wait for 800 MB free.
  - The stale lock the killed run left behind wedged every deploy. PR #561 fixed that and is on main.
  - I did not touch the build path, so the two grants don't collide.
- **The adoption fix (PR #564):**
  - `takeAdoptable` now returns null when there is no handover, when the file is stale, or when it can't be read.
  - On null, the runtime adopts every running docker work session on probation.
  - The desk's first control poll (it polls every 3 s) or activity makes it a normal adopted session. The existing 5 min and 30 min silence rules then apply.
  - A session not heard within `ADOPT_GRACE_MS` (2 min) is cut exactly as before: `interrupted`, "cut by restart", assignment back to pending, desk process killed through `killOrphan`.
  - Host sessions are still cut by reconcile, because they die with the process.
  - A clean handover still adopts only the sessions it lists.
- **Verified:**
  - Runtime tests pass: 276 of 276, including 4 new "unclean restart" tests in adopt.test.ts. 3 startup-reconcile tests in v12.test.ts were rewritten to match the new rule.
  - `npm run check --fast` passes: docs, deadcode, typecheck and tests.
- **kr_bl7iymrj2c:** the CI part is done once #564 is merged. The live part needs the next unclean restart, which should show an "Adopted … after an unclean restart" event and those sessions ending done.

## What I need from you
Nothing needed.
