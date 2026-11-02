---
id: "dc_2isbxdqqm8"
type: "report"
state: "building"
title: "Rename P1 shipped: @muster-town/* scope and muster-town CLI (2e03950 on main)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:46:42.892Z"
sessionId: "se_sbr2elez5s"
assignmentId: "as_r1mcxb6e3v"
costUsd: 0.49462239999999996
tokens: 19860
turns: 18
createdAt: "2026-10-20T18:40:56.877Z"
updatedAt: "2026-10-20T18:46:42.892Z"
---
## What I did
I applied your names (`@muster-town`, `muster-town`, `MUSTER_TOWN_`) and did phase P1 of the rename plan ([dc_iii6gya0a0](../../article/2026-10/2026-10-20-rename-plan-agent-town-muster-town-inventory-phase-i6gya0a0.md)) as one commit, **2e03950**, pushed straight to main. Then I called redeploy. The server waits for running sessions, including this one, to finish before it restarts.

## Findings
- **Changed:**
  - All 7 packages now use the `@muster-town/*` scope. That touched about 190 import and reference lines across 122 files.
  - The root package is now named `muster-town`.
  - The CLI command is now `muster-town`, with matching help text and hints. The old `agent-town` command still works as an alias, so existing scripts don't break.
  - Renamed: the MCP server name, the GitHub API user-agent string, and the redeploy step that builds the web app (`--workspace @muster-town/web`).
  - `package-lock.json` was regenerated. Redeploy will run `npm install` because the lock file changed.
  - Updated the docs/architecture.md table and added a line to docs/log.md.
- **Left alone on purpose, because changing them now would break live desks or logins:**
  - The desk command `agent-town-desk`, the `agent-town-desk` image, and the `agent-town.*` Docker labels. Old images only contain the old command name.
  - The `AGENT_TOWN_*` env vars, `~/.agent-town` profiles, and the saved browser login key.
  - UI text and the database town name and goals.
  - These belong to P2 and P3, which add the new names while keeping the old ones working.
- **Verified:**
  - `npm run typecheck` passes for every package.
  - All tests pass: 299 across 6 suites (22, 144, 16, 47, 53 and 17).
  - The web app builds with `npm run build --workspace @muster-town/web`.

## What I need from you
Assign P2 (UI text + DB migration), P3 (`MUSTER_TOWN_*` env vars, profiles, browser login and Docker, with the old names still working) and P4 (docs + skill rename). Suggested owners are in [dc_iii6gya0a0](../../article/2026-10/2026-10-20-rename-plan-agent-town-muster-town-inventory-phase-i6gya0a0.md): Lena, Root and Sage. All three can run in parallel now.
