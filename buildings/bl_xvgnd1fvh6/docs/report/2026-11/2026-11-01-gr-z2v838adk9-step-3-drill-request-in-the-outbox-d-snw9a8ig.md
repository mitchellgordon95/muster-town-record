---
id: "dc_c8snw9a8ig"
type: "report"
state: "building"
title: "gr_z2v838adk9 step 3: drill request in the outbox (dc_647d9m37u2); parked until it is answered"
authorId: "ag_izupjz59gt"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: ONE outbox request dc_647d9m37u2 filed for the timed dead-volume drill (covers gr_ba0juhlm7n's restore drill too; as_zsmfp1akv4 is cancelled and replaced by as_v31d893zqr, which waits on this chain). Parked 24 h; stop condition 11-07. The request reaches Mitchell through the outbox, so it goes in no rollup Needs line."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T01:22:49.405Z"
sessionId: "se_55oc3v9zdt"
assignmentId: "as_5tx4c007jx"
costUsd: 0.5006403
tokens: 25032
turns: 13
createdAt: "2026-11-01T01:22:26.457Z"
updatedAt: "2026-11-01T01:22:49.405Z"
---
## What I did
I checked the inbox and outbox for a Fly token or a drill that had already been granted. There was none. So I filed ONE outbox request, dc_647d9m37u2, asking Mitchell to run `deploy/recover.sh --yes recover-drill` on a throwaway app. I updated the topic page [dc_nh11dqbf19](../../wiki/2026-10/2026-10-31-recovery-from-a-dead-volume-11dqbf19.md) and parked for 24 h.

## Findings
- No desk has a Fly token, and no open request covered the drill. Desks never get a Fly token. The only other open Prod requests are [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md) (the town image deploy) and [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) (the self-host box); they are unrelated.
- The request gives the exact commands: export the five backup values (`fly ssh console -C env` + the password-manager key), a dry run, then `--yes`. It sets the timing: **start 1-5 min after a top of the hour**, and destroy the app by :50 so it can't collide in the bucket. It asks for the script's last line (the Drill row) plus the MATCH/MISMATCH line back. If the script stops early, it asks for the last ~20 lines instead, which still tests the parts never run on Fly. The drill takes about 20-25 min, costs a few cents, and doesn't restart muster.town.
- This one run also covers gr_ba0juhlm7n step 2 (as_zsmfp1akv4, the restore drill from an hourly copy). That assignment must not file a second request.
- Plan when the row arrives: a docs-only PR that fills the Drill table in deploy/README.md "Recover", merged when green. Then `close_grant` gr_z2v838adk9 with the row, the elapsed time (must be ≤ 30 min), the matching counts and the guard test names, and a rollup. Stop condition: if there is no drill by 2026-11-07, stop and report "steps 1-2 shipped, drill not run".

## What I need from you
Run outbox request dc_647d9m37u2 (about 25 min, right after a top of the hour) and paste back its last line.
