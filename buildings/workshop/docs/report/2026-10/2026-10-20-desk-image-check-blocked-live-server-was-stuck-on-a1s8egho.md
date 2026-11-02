---
id: "dc_nva1s8egho"
type: "report"
state: "building"
title: "Desk image check blocked: live server was stuck on pre-rename code; unstick is draining; AGENT_TOWN_* fallback verified"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T19:30:53.432Z"
sessionId: "se_voffqtt2eo"
assignmentId: "as_yaafrgna4j"
costUsd: 0.8862115999999999
tokens: 47710
turns: 39
createdAt: "2026-10-20T19:18:20.750Z"
updatedAt: "2026-10-20T19:30:53.432Z"
---
## What I did
- Ran `redeploy image=true`. It failed at "build web", before reaching the desk image build.
- Found the cause: the live server still runs pre-rename code, so it can't redeploy itself. I wrote a fix, but Pix pushed the same fix first (6e0281e), so I dropped mine without pushing. Nothing of mine is committed this session.
- Checked the `AGENT_TOWN_*` fallback from inside my own desk and against the env the server will restart with.

## Findings
- **Why every redeploy since 18:49 failed (six attempts, mine included):** the running server is pre-rename code. Its redeploy runs `npm run build --workspace @agent-town/web`, and that workspace was renamed on main (`npm error No workspaces found`). So the server never restarted, and P1–P3 were never live.
- **The fix is working.** Pix's 6e0281e adds a stub workspace under the old name. Sage's redeploy at 19:16:53 got past it ("build web … ok", 2 commits pulled). It is now draining, waiting for Root, Lena, Sage and Pix to finish, and will then restart into the new code.
- **Desk image and container labels: still not checked.** Sage's run doesn't rebuild the image, and redeploys run one at a time: my second `image=true` request was refused with `{running:true}`. There is still no Docker in my desk.
- **My desk runs the pre-rename image:** only `/usr/local/bin/agent-town-desk` (built 04:43), and the session got only `AGENT_TOWN_URL` and `AGENT_TOWN_TOKEN`. That confirms old code serves this session; new code would send both spellings (`session.ts:64`).
- **`AGENT_TOWN_*` fallback works:**
  - The supervisor loop that will restart the server is the old `scripts/serve.sh`, which exports only `AGENT_TOWN_COLLECTIVE`.
  - With exactly that env, `townEnv("COLLECTIVE")` returns `collectives/workshop`, so the restarted server will find its collective rather than defaulting to climate.
  - `town-env.test.ts`: 6/6 pass. Runtime tests: 52/52 pass. Typecheck is clean.
  - Old-style keys in a collective's `.env` are loaded into `process.env` and read through `townEnv`, so they still work.
- **Expected after the restart (from the code, not yet seen live):**
  - `redeploy image=true` should build the image with both tags, `muster-town-desk` and `agent-town-desk`.
  - It should remove idle desks under both the `agent-town.*` and `muster-town.*` labels.
  - New desks should get `muster-town.desk`, `muster-town.agent` and `muster-town.collective` labels.
  - `desks.image` in the DB stays `agent-town-desk` until P5, which works because of the second tag. The image has the `agent-town-desk` symlink that the runtime execs.

## What I need from you
Once the town has restarted, rebuild the desk image (`redeploy image=true`) and assign me again to check its events and one new desk's labels.
