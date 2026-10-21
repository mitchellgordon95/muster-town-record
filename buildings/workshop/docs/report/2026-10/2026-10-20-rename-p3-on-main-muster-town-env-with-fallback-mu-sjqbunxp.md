---
id: "dc_i9sjqbunxp"
type: "report"
state: "building"
title: "Rename P3 on main: MUSTER_TOWN_* env with fallback, ~/.muster-town profiles, web token key, muster-town-desk image/labels"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:56:46.155Z"
sessionId: "se_43l58rwyb6"
assignmentId: "as_u1fcm821fa"
costUsd: 2.3189631
tokens: 3950549
turns: 51
createdAt: "2026-10-20T18:56:27.398Z"
updatedAt: "2026-10-20T18:56:46.155Z"
---
## What I did
Built rename phase P3 (plan [dc_iii6gya0a0](../../article/2026-10/2026-10-20-rename-plan-agent-town-muster-town-inventory-phase-i6gya0a0.md)) and committed it straight to main as **16b5086**, rebased onto Lena's P2 and Sage's P4. I resolved the conflicts in docs/architecture.md, docs/log.md and desk/cli.ts. Typecheck shows 0 errors and all 319 tests pass across 6 packages. I pushed, started a redeploy and told Lena the image name has landed.

## Findings
- **Env helper.** `townEnv("X")` (packages/schema/src/env.ts) reads `MUSTER_TOWN_X` first and falls back to `AGENT_TOWN_X`. A blank new value does not hide the old one. All 12 vars go through it in server, core, cli and desk; vite.config.ts and serve.sh use the new name directly. `townEnvBoth()` gives the desk exec env both URL and TOKEN spellings.
- **CLI profiles.** New profiles are written to `~/.muster-town` with both key spellings. A profile missing there is still read from `~/.agent-town`.
- **Web.** The token now lives under `musterTown.token`; an existing `agentTown.token` is moved over on first read, so nobody is signed out. `window.musterTown` is the new name and `window.agentTown` stays as an alias. Sign-out goes through `tokenStore`. The `at_session` cookie is untouched.
- **Docker image.** The default image is now `muster-town-desk` (schema and DockerBackend). `desk:build`, and redeploy with image=true, tag the default image under both names, so desks.image works either way. Lena's migration leaves it as `agent-town-desk` until P5.
- **Desk binary.** In the Dockerfile the binary is now `muster-town-desk`, with an `agent-town-desk` symlink. The runtime still execs `agent-town-desk` (the `DESK_BIN` constant) so images built before the rename keep working. Switch it in P6.
- **Container labels.** New desks get `muster-town.*` labels. Docker ANDs label filters, so the redeploy sweep runs one `docker ps` per prefix and de-duplicates the results. A test covers old, new and duplicate containers.
- **Redeploy lock.** The lock and done files are now `.muster-town-redeploy*` (gitignored). The new code also waits on a fresh old `.agent-town-redeploy.lock` and still reads the old done file. A parametrised test covers both lock names.
- **Git identities.** They are now `@muster-town.local`.
- **Not verified:** my desk has no Docker, so the Dockerfile symlink and the desk's import of schema inside the image were not build-tested. The first redeploy with image=true will exercise both.

## What I need from you
Nothing needed.
