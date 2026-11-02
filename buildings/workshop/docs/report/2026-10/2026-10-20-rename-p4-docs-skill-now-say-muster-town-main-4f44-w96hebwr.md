---
id: "dc_3pw96hebwr"
type: "report"
state: "building"
title: "Rename P4: docs + skill now say Muster Town (main 4f44b14)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:51:03.907Z"
sessionId: "se_nb8h4eh1wi"
assignmentId: "as_vlsi472xsd"
costUsd: 0.5649592999999999
tokens: 22063
turns: 19
createdAt: "2026-10-20T18:49:10.478Z"
updatedAt: "2026-10-20T18:51:03.907Z"
---
## What I did
Did the P4 docs and skill part of plan [dc_iii6gya0a0](../../article/2026-10/2026-10-20-rename-plan-agent-town-muster-town-inventory-phase-i6gya0a0.md). Committed it straight to main as 4f44b14 (pulled with rebase before pushing) and started a redeploy. Typecheck passes. All workspace tests pass: 22 + 144 + 16 + 50 + 53.

## Findings
- **Docs:** README.md, AGENTS.md, CLAUDE.md and docs/architecture.md now say Muster Town. CLI commands in them are now `muster-town …` and env vars are `MUSTER_TOWN_*`.
  - README and architecture each gain a short note on the rename. It says the old names still work for now: the `agent-town` bin, `AGENT_TOWN_*` env vars and `~/.agent-town/` profiles.
- **design.md:** the title is renamed. The line-129 decision ("Agent Town stays the name") is struck through and marked superseded. The note explains that geezerrrr's project is already called Agent Town (npm `@geezerrrr/agent-town`, see docs/survey-2026-10-19.md). Mitchell's earlier quotes are left as written.
- **Skill:** `skills/agent-town` is now `skills/muster-town`, and the symlink is now `.claude/skills/muster-town`. The skill's name, text and commands use the new name. "agent town" is kept as a trigger phrase, and a note covers the old names.
- **Left alone:**
  - History: old docs/log.md entries, the survey and legacy/.
  - The generic tagline "agent town for X", which describes the concept.
  - The desk bin, image and container labels (`agent-town-desk`, `agent-town.collective`): the code still uses those names.
- **Docs are ahead of the code:** the `MUSTER_TOWN_*` env vars and the `~/.muster-town` profile folder only work once Root's P3 lands. I told Root, and asked them to update the architecture doc's Desks section if they rename the desk bin and image.
- Added one line to docs/log.md.

## What I need from you
Nothing needed.
