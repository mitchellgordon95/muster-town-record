---
id: "dc_g8gwigr4sy"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Secretary — notes"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-13T23:28:43.387Z"
updatedAt: "2026-11-13T23:28:43.387Z"
---
# 1:1: Mitchell and Secretary

Kind: one-on-one. Facilitator: Secretary. Attendees: Secretary. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Secretary:** Hi Mitchell. 12 asks are open, two credentials at the top (the image deploy and the self-host box). What do you need?
- **Mitchell:** ok i can do this but i still don't understand why i have to do it and it's not party of CI
- **Secretary:** Fair question. Two layers of deploy here, and CI only owns one.

The town's `redeploy` (what CI calls on every green main, ci.yml:97) is a `git pull` inside the running Machine: it updates the checkout on the volume, not the image. The two 503 fixes (prebuilt-JS entrypoint from PR #230, the 10 s health-check timeout in fly.town.toml) live in the image and the Fly config, which only `fly deploy` changes (Dockerfile:5, deploy/README.md:316).

Why CI doesn't run `fly deploy`: nobody has given it a Fly token for the muster-town app. CI holds only MUSTER_TOWN_DEPLOY_TOKEN, a town token (ci.yml:65). It does build the image every green main and pushes it to ghcr (ci.yml:100-132), but it never deploys it to Fly. The server's own FLY_API_TOKEN is the desks app's deploy token only (deploy/README.md:24), so the town can't do it either. That leaves your Mac, which has `fly auth login`.

If you want this to stop landing on you: create a Fly deploy token for muster-town, add it as a GitHub Actions secret, and someone adds a `fly deploy` step to the image job. That is a one-time credential ask, and this card would be the last of its kind. Want me to file that as its own ask to Prod?
- **Mitchell:** yes
- **Secretary:** Done. A new credential ask is in your queue: create a Fly deploy token scoped to the muster-town app and add it as the GitHub Actions secret FLY_TOWN_DEPLOY_TOKEN. I told Cleo to add the fly deploy step to CI's image job once the secret exists. Recorded as decision 1 here.

This one on your screen still needs the one manual run of build.sh for now. Mark it Done after you run it.
- **Mitchell:** wait ok i want to understand more about our deployment situation here. so what does Fly give us? we hand it a docker image and it runs the containers, right?

so what you're telling me is that the container then github clones the code and runs it? and a deploy just runs git pull and restarts the server

then what even lives in the image that needs updating?
- **Secretary:** Yes, you have it right. Fly runs one Machine from our Docker image with a persistent volume at /data. The image is deliberately thin: node 22, git, build tools, sqlite3, plus a baked copy of main as a first-boot seed (Dockerfile:4-20). On the very first boot, entrypoint.sh copies that seed to /data/repo on the volume (entrypoint.sh:16-20). After that the image's copy is never used again: the live code is the checkout on the volume, and the town's `redeploy` does git pull, npm install, build, exit 75, and the entrypoint loop restarts the server (entrypoint.sh:72-85). So yes: a normal deploy is a git pull and a restart.

What actually lives in the image and only changes with `fly deploy`:

1. entrypoint.sh itself. It is copied into the image at build (Dockerfile:22), not read from the checkout. The live image's entrypoint still runs `npx tsx packages/server/src/main.ts`, compiling TypeScript at every boot. The new one (PR #230) looks for deploy/fly/start-server.sh in the checkout and runs prebuilt JS instead (entrypoint.sh:70-78). That file is already on the volume via git pull, but the old entrypoint never looks for it.

2. fly.town.toml. That is not even in the container, it is Fly's config: [env] vars, the VM size, and the health check. The 10 s check timeout (fly.town.toml:43) and 240 s grace period are applied by `fly deploy`. The live Machine still has the old 5 s timeout, which is what turned a slow /api/health into a 503 at the edge.

3. The runtime base: node version, apt packages. Rarely changes.

So `redeploy` covers all the app code. `fly deploy` covers the supervisor script, the Fly config and the OS layer. Those three change maybe once a month, which is why it was tolerable to leave them to a Mac command. The CI step fixes that properly.
- **Mitchell:** didn't we already run this one through wright?
- **Mitchell:** hello?

## Decisions

1. Image deploys move into CI. Mitchell creates a Fly deploy token for the muster-town app and adds it as the GitHub Actions secret FLY_TOWN_DEPLOY_TOKEN (ask ak_yhxjzh3m7x). Prod adds a fly deploy step to the image job (told Cleo, en_ev155825_relay). The current one-off image deploy (ak_lngn51c7ow) still runs once by hand.

