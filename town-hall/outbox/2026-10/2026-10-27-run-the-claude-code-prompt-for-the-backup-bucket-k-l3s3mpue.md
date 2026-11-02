---
id: "dc_1ul3s3mpue"
type: "request"
state: "building"
title: "Run the Claude Code prompt for the backup bucket, key and restore drill (Prod, gr_jkorz4f49a)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["other"]
requestStatus: "done"
claimedByUserId: "us_1la74k332n"
createdAt: "2026-10-27T17:46:24.744Z"
updatedAt: "2026-10-28T18:51:47.318Z"
---
**What:** copy the prompt in [dc_go7ux3qzjb](../../../buildings/bl_xvgnd1fvh6/docs/note/2026-10/2026-10-27-prompt-for-claude-code-create-the-backup-bucket-se-7ux3qzjb.md) (Prod filing cabinet, "Prompt for Claude Code: create the backup bucket, set the key...") into a Claude Code session on your Mac and let it run. It creates the Tigris bucket on muster-town, generates the backup key (it stops once so you save the key in your password manager as "muster-town backup key"), confirms `backup.lastAt` on https://muster.town/api/health, runs `scripts/backup/restore.sh` (local check, then a scratch app muster-town-restore that is destroyed at the end) and fills the Drill line in deploy/README.md on main.

**Why:** it is the last thing the backup key result kr_giqd28iwcb needs. The code (nightly encrypted copy, health field, restore script) has been live since 2026-10-27 but is switched off until the five secrets exist, and only you can create the bucket and hold the key. Today the Fly volume is the only copy of the live world.

**How:** needs flyctl logged in, node 22.6+, gh or your SSH key for the repo, about 20 minutes, two 30 s restarts of muster.town and roughly $0.05 of Fly time. At the end Claude Code prints one summary block: paste it to Cleo in the town (or just the README commit sha) and I file the evidence report.
