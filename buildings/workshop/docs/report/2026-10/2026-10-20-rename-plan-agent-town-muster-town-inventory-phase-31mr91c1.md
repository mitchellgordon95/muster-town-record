---
id: "dc_wr31mr91c1"
type: "report"
state: "building"
title: "Rename plan Agent Town → Muster Town: inventory, phases, split (dc_iii6gya0a0)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "@muster-town, muster-town, MUSTER_TOWN_"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:30:18.595Z"
sessionId: "se_es7rcu6r2i"
assignmentId: "as_oof2znurit"
costUsd: 0.6380282
tokens: 436858
turns: 13
createdAt: "2026-10-20T18:25:08.440Z"
updatedAt: "2026-10-20T18:30:18.595Z"
---
## What I did
I grepped every tracked file on main @ 503ce2b for `agent[ _-]?town` and traced how the town name and goals get into the live database. I wrote up the full inventory, the phases and a proposed task split in **[dc_iii6gya0a0](../../article/2026-10/2026-10-20-rename-plan-agent-town-muster-town-inventory-phase-i6gya0a0.md)** (filing cabinet). I changed no code, so there was no commit or redeploy.

## Findings
- **Scale:** about 470 hits in 100 of 254 files. I sorted them into six groups: display text, live database data, package scope and command names, environment variables and config, docs and skills, and the GitHub repo and URLs.
- **Live data is the main risk:** the town name, goal and tagline, the building goals, and the desk image name are copied into the database once, on first boot. After that, editing `collective.json` does nothing, and no command updates the town or building goal. The rename needs a migration that rewrites those fields only where they still say "Agent Town". Old reports and documents stay as history.
- **Package rename:** the 7 packages are all called `@agent-town/...`, with about 200 imports. They aren't published to npm, so the rename stays inside the repo. It still touches about 100 files, so it should be one commit, done first, with nobody else working in the tree.
- **Must keep the old names working for a while:**
  - 12 `AGENT_TOWN_*` environment variables (`TOKEN` appears 50 times, `URL` 34) and `~/.agent-town` CLI profiles.
  - The saved browser login key `agentTown.token`.
  - Docker labels `agent-town.*`: redeploy finds old desk containers by this label, so it must match old and new labels for one release, or old desks are left behind.
  - Leave the session cookie name alone; renaming it signs everyone out.
- **Phases:**
  - P0: Mitchell decides the names.
  - P1: one atomic commit for the package names and command names.
  - P2–P4, in parallel after P1: P2 UI text plus the database migration; P3 compatibility for env vars, profiles, browser login and Docker; P4 docs and the skill rename.
  - P5: switch over on the host (GitHub repo rename, `.env` keys, rebuild the desk image).
  - P6: about a week later, remove the old-name fallbacks.
- **Suggested owners:** P1 Pix, P2 Lena, P3 Root, P4 Sage, P5 Claude Code or Mitchell. This needs a standup to assign. I couldn't schedule a meeting myself.

## What I need from you
Decide the P0 names (package scope `@muster-town`? command `muster` or `muster-town`? env prefix `MUSTER_TOWN_` or `MUSTER_`? rename the GitHub repo?), then put the split on the next standup's agenda.

## Reply from Mitchell (2026-10-20 14:30)

@muster-town, muster-town, MUSTER_TOWN_

