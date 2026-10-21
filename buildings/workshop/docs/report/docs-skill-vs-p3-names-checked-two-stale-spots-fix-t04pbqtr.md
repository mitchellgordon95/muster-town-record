---
id: "dc_46t04pbqtr"
type: "report"
state: "building"
title: "Docs/skill vs P3 names: checked, two stale spots fixed (main 7482252)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T19:17:27.470Z"
sessionId: "se_sfjwmp0nu2"
assignmentId: "as_jttly83zfn"
costUsd: 0.5751352
tokens: 712816
turns: 19
createdAt: "2026-10-20T19:17:02.119Z"
updatedAt: "2026-10-20T19:17:27.470Z"
---
## What I did
I compared every env var, path, bin, image and label name in README, AGENTS/CLAUDE.md, docs/architecture.md, docs/design.md and skills/muster-town (SKILL.md, README) against the code on main after P3 (16b5086). I fixed the two spots that didn't match, then ran typecheck and the server tests (53/53 passed). I pushed straight to main as **7482252** and started a redeploy. Lena's pass hadn't reached main when I pushed (origin/main had nothing past 16b5086), so I checked against P3 alone.

## Findings
- **Matches the code:** all 12 `townEnv` names (the `MUSTER_TOWN_*` → `AGENT_TOWN_*` fallback), the `~/.muster-town` → `~/.agent-town` profile fallback, the `muster-town`/`agent-town` CLI bins, the `muster-town-desk` image and its old tag, the desk bin alias, the `muster-town.*` labels plus the old-prefix sweep, the `.muster-town-redeploy-done-*` file, and the `.claude/skills/muster-town` symlink.
- **Fixed, `docs/architecture.md:9`:** it still said the desk bin, image and labels "still carry the old name". It now says they use the new name, and that the runtime still execs the old bin name and sweeps both label prefixes for desks built before the rename.
- **Fixed, `packages/server/src/main.ts` header comment:** it listed PORT among the prefixed vars, which suggested `MUSTER_TOWN_PORT` exists. It doesn't. PORT and HOST are plain env vars.
- **Left alone on purpose:**
  - `MUSTER_TOWN_HOME` and `MUSTER_TOWN_GITHUB_URL` are test hooks, so the user docs don't mention them.
  - The image's internal `/opt/agent-town` directory isn't user-facing; it fits P6 cleanup.

## What I need from you
Nothing needed.
