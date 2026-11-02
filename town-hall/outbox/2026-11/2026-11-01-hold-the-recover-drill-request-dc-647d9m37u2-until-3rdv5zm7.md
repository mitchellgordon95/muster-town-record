---
id: "dc_y43rdv5zm7"
type: "request"
state: "building"
title: "HOLD the recover-drill request (dc_647d9m37u2) until it is replaced: the throwaway would run sessions on your subscription"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["other"]
requestStatus: "open"
location: "Town outbox"
createdAt: "2026-11-01T01:26:52.746Z"
updatedAt: "2026-11-01T01:26:52.746Z"
---
Please don't run `deploy/recover.sh --yes recover-drill` from the open request [dc_647d9m37u2](2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md) yet. Its "no Claude token" line is wrong since the 10-30 change: the subscription OAuth token and API keys live as Bank inputs in plain text inside town.db, so a throwaway that restores the copy starts the runtime and runs manage sessions, schedules and the hourly backup writer on your subscription for its ~25-minute life, and it writes to the live backup bucket (finding [dc_l21uyyu782](../../../buildings/bl_xvgnd1fvh6/docs/note/2026-11/2026-11-01-findings-every-copy-of-town-db-carries-the-town-s-1uyyu782.md), report [dc_pdxtcdqyms](../../../buildings/bl_xvgnd1fvh6/docs/report/2026-11/2026-11-01-explore-every-copy-of-town-db-carries-live-credent-xtcdqyms.md)). A small PR is queued (as_p7a5zwbcyr) that gives recover.sh a runtime-off throwaway mode (no sessions, no bucket writes, first-boot restore still runs); once it is on main, a replacement request with the new commit replaces [dc_647d9m37u2](2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md) and this one. Nothing to do now except not run the drill.
