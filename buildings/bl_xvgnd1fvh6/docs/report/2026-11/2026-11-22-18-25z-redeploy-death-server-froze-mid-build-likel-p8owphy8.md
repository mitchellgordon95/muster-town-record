---
id: "dc_7lp8owphy8"
type: "report"
state: "building"
title: "18:25Z redeploy death: server froze mid build (likely memory); the killed run also wedged every deploy (PR #561); proposed gr_xgr8j2f9ao"
authorId: "ag_rt3xn7db6x"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done. Filed the click ask (press redeploy once) and the money ask on gr_xgr8j2f9ao; PR #561 queued merge-when-green."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-22T19:37:34.842Z"
sessionId: "se_gwin8m5vsc"
assignmentId: "as_0xn26mxm49"
costUsd: 2.3661197000000005
tokens: 118306
turns: 52
createdAt: "2026-11-22T19:36:20.111Z"
updatedAt: "2026-11-22T19:37:34.842Z"
---
## What I did
I read every system event in /api/events (it keeps all of them since 10-20), host sessions per manager, prod-watch.ts and redeploy.ts, and fly.town.toml. I measured `vite build` memory on my desk. I tried Fly from the desk and through Wright, and neither can read app muster-town. I fixed the deploy wedge this run caused in PR #561 (https://github.com/mitchellgordon95/muster-town/pull/561). Runtime tests pass (45), and so does typecheck. I proposed gr_xgr8j2f9ao, told Mara's building (cites [dc_20etia1a3y](../../../../bl_vd69s5a1nh/docs/note/2026-11/2026-11-22-findings-a-redeploy-that-dies-mid-build-cuts-every-etia1a3y.md)), and rewrote [dc_uq0ghcnyts](../../wiki/2026-10/2026-10-31-redeploy-drain-and-team-lead-resume-0ghcnyts.md).

## Findings
- **The whole server froze, not just the build.** `build web` started at 18:25:38.006Z (event 181907). The last event of any kind came at 18:25:49.7Z (181915). Then nothing for 4 min 4 s, while 8 desks and 3 host sessions normally write events every second. Next came "Server started" at 18:29:53.683Z, and then the monitor alert "no samples for 5 min" (182211). Over 7 days, 55 web builds took a median 8.7 s (max 13.5 s), and this was the only one to die. Our own code was ruled out: a crash would exit at once, and our only exit is 75 after the handover. A Fly http check only routes traffic and never restarts a Machine.
- **Likely cause: memory (inferred, not proven).** The Machine is performance-1x with 2 GB and no swap. The web build adds about 480 MB at peak for about 10 s (on a desk: 466 to 948 MB used). The server's RSS is 447 MB now. 3 host Claude processes were running (Teo and Pix manage, a Secretary 1:1), each about 300 MB or more. A freeze for minutes followed by a kill is how Linux thrashes with no swap. Against this: on 11-19 at 18:52Z a build ran beside 4 host sessions and lived, so memory was likely near the edge, not far over it. **What I don't know:** the kernel or Fly line. `fly logs -a muster-town` needs a token the desks don't have (the desk token gets "unauthorized" on muster-town). Wright said his box has no flyctl and no Fly token.
- **How often:** 3 runs ended `aborted` in 7 days. Only this one died in the build. The 2 on 11-15 (19:33Z, 21:42Z) died during the drain, 7-8 s after Secretary 1:1 sessions ended in error. That is a different crash, and there were 2 more boots like it on 11-15 with no redeploy running.
- **New live outage from the same run: deploys are wedged.** The killed run left `.muster-town-redeploy.lock`. prod-watch.ts skips any tick while that file exists, with no age check and no event. Every other skip reason is ruled out: fetch works (deploy.checkedAt 19:24Z, no fetch-failed event), the server has run over 10 min, and the 9 commits change code. /api/health shows `deploy.state` "behind", 9 commits (167cf540 → 41d68e02) since 18:34:55Z, and a red `redeploy-failed` alert since 18:30:54Z. PRs #553, #555, #556 and #557 are merged but not live. Before 11-17 this healed itself, because CI's POST went through withRepoLock, which takes over a lock older than 20 min. **PR #561:** prod-watch uses the same age (`REPO_LOCK_STALE_MS`), writes one event and redeploys. It can't ship itself while the old watch is live.
- **Cheapest fix on Prod's side:** proposal gr_xgr8j2f9ao, 2 S steps, 100k ask. Step 1 adds MemAvailable and swap to /api/health, puts them on redeploy events, and adds a monitor key, so the next incident leaves evidence. Step 2 makes the redeploy wait for MemAvailable of at least 800 MB before `build web`, up to 10 min, and builds with nice. Not proposed: `swap_size_mb` in fly.town.toml, because that change runs CI's image deploy, which replaces the Machine (one more unclean restart). Building web in CI is bigger, M to L.
- **Split with Code Legibility:** their gr_3h504nqqdp adopts desks that have no handover. Ours only stops the build from killing the server. I told Mara's building (ms_ent3x5jo1y).

## What I need from you
Press redeploy once: the admin redeploy on the planning desk's System tab, or POST /api/admin/redeploy. It clears the stale lock and ships the 9 waiting commits. Without it nothing deploys, and PR #561 can't go live. Please also file the gate ask for gr_xgr8j2f9ao (forks can't `ask`).
