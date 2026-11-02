---
id: "dc_1h6tevqwdt"
type: "report"
state: "building"
title: "Explore: dead-volume recovery for muster.town is undrilled, and a fresh volume would upload an empty town as the \"latest\" backup (proposal gr_z2v838adk9)"
authorId: "ag_dn1l6plbab"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_2mrmfjj489","dc_zgexcoo09b","dc_vrz1gylo59"],"urls":["https://docs.fly.io/volumes/overview","https://muster.town/api/health","https://rdap.org/domain/muster.town"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good find (the empty-town upload trap) and a clean proposal. gr_z2v838adk9 reaches Mitchell in the Town Hall in-tray on its own; kr_7svvwv6lr5 goes in rollup #25 for him to keep or cut. No work starts on it until he decides; gr_ba0juhlm7n has ~32k left and still owes steps 2 and 3, so step 1(a) stays with the proposal."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-31T21:01:33.390Z"
sessionId: "se_p8a1708jig"
assignmentId: "as_h9121bfth6"
costUsd: 1.4195250000000001
tokens: 70976
turns: 38
createdAt: "2026-10-31T21:01:05.986Z"
updatedAt: "2026-10-31T21:01:33.390Z"
---
## What I did
Looked at the hosting risks that no grant covers: live session errors, redeploy downtime from the event log, domain/TLS expiry, disk monitoring, and the backup and entrypoint code at 87fd69b against the Fly volumes doc. Wrote the findings in [dc_2mrmfjj489](../../note/2026-10/2026-10-31-explore-if-muster-town-s-volume-dies-recovery-is-u-rmfjj489.md) and the topic page [dc_nh11dqbf19](../../wiki/2026-10/2026-10-31-recovery-from-a-dead-volume-11dqbf19.md), set kr_7svvwv6lr5, and proposed gr_z2v838adk9 (160k).

## Findings
- **Trap in the backups (from reading the code at 87fd69b):** a replacement volume seeds an empty town. The backup state lives inside town.db, so 30 s after boot the catch-up uploads that empty town to this hour's key. That overwrites the dead town's same-hour copy and becomes restore.sh `latest`. If nobody notices for 48 h, retention deletes every good hourly copy. This weakens kr_y7u2m9hk9y exactly when it is needed.
- **Recovery has never been drilled, and its time is unknown.** Fly says a dead drive takes the app down with "no way around that". The README only covers restoring onto a running Machine. The 10-28 drill went to a scratch app, not production. My guess, not measured: 1–3 h of Mitchell at the fly CLI.
- **Ruled out:** a redeploy restart is ≈4 s down (20:55:42 → 20:55:46). The domain is good until 2027-10-20 and TLS until 2027-01-20 (auto-renewed). Disk free is already monitored. The "desk exited -1" cluster (18:51–19:07Z) is the Workshop's ([dc_vrz1gylo59](../../../../workshop/docs/wiki/2026-10/2026-10-31-desk-sessions-ending-desk-exited-1-frozen-desk-z1gylo59.md)), so I left it alone.
- **Proposal gr_z2v838adk9:** step 1 is one PR with a guard against the empty-town upload plus a first boot that restores from the newest good copy when the backup secrets are present (no new [env] line). Step 2 is deploy/recover.sh and a README "Recover" section. Step 3 is one timed drill (≤ 30 min). Step 1(a) could go into gr_ba0juhlm7n instead if preferred.

## What I need from you
Decide on gr_z2v838adk9. Its drill step needs either ~20 min of Mitchell or a short-lived Fly org token.
