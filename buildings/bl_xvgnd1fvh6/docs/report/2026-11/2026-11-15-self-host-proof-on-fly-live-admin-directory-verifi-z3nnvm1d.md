---
id: "dc_2uz3nnvm1d"
type: "report"
state: "building"
title: "Self-host proof on Fly: live, admin, directory-verified, torn down; docs PR #456 parked on CI"
authorId: "ag_yf92r547yc"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Passed up to the humans as ask ak_w2a95k32je: Self-host path B proven on the throwaway app (health, admin token, 3 restarts, directory verified) and torn down; PR #456 continuation as_u770oxyn16 already waits on its CI. The only open item is Mitchell's: destroy the suspended app and revoke the token, passed up as a do ask."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-15T20:58:28.406Z"
sessionId: "se_szpbeygqkn"
assignmentId: "as_uskv4clzoe"
costUsd: 1.6324968000000002
tokens: 81625
turns: 41
createdAt: "2026-11-15T20:57:34.442Z"
updatedAt: "2026-11-15T20:58:28.406Z"
---
## What I did
I brought up a town on the throwaway Fly app `muster-town-selfhost`, using docs/self-host.md path B: the published `:prod` image, no clone and no build. I checked health, the admin token and restarts. I registered the app with muster.town's directory and got it verified. I fixed the doc in PR #456 and tore the app down. I am parked on #456's CI.

## Findings
- **Live:** https://muster-town-selfhost.fly.dev/ (now gone).
  - Health showed `ok:true`, commit dc6a38003d2c, startedAt 2026-11-15T20:51:11.700Z, then 20:52:40.666Z after my restart.
  - It ran one shared-cpu-2x 2 GB machine with a 1 GB volume. First boot took ~52 s.
  - Screenshot: mf_399l96gycx.
- **Admin / first sign-in:** the admin token (read with `fly ssh console`) returned roles `admin` and the town-hall manager on /api/me. GitHub sign-in was not tested: there is no OAuth app, and that stays in known gap 4.
- **Restarts:** after 3 restarts (machine restart ×2 and a secrets set), the logs say "opened collective … from /data/mytown/data" each time, and the admin token still works.
- **Directory:** register, then `MUSTER_TOWN_DIRECTORY_TOKEN` as a Fly secret, then the well-known URL served the token. `/verify` gave `status: verified, proof: well-known, verifiedAt 2026-11-15T20:55:10.037Z`, and the town appeared in `GET https://muster.town/api/directory`. The row will delist itself after a day unseen.
- **Doc gaps fixed in PR #456** (https://github.com/mitchellgordon95/muster-town/pull/456; docs only, check:docs ok):
  - Section 6 still said the directory was "being built". It now covers the verify call, re-check and delist rules, and the per-IP limits.
  - A 6-line "On Fly.io" note under path B. Fly writes `[[files]]` before it mounts the volume, so collective.json must sit outside /data. This is the likely cause of the failed v1 release.
  - Known gap 4 is now "partly proven", gap 9 is struck, and a new gap 10 records that the Uptime block says "Measured by UptimeRobot" even with no key set.
  - Log entry added in docs/log.d.
- **Teardown (20:56Z):** 0 machines. The volume is in `scheduling_destroy`. The app is *suspended, not destroyed*: `fly apps destroy` with the deploy token fails with "Not authorized to access this addon".
- **Cost:** the machine ran ~15 min (about 20:43–20:56Z) and the volume ~13 min. At Fly's list price (~$12/month for shared-cpu-2x 2 GB; I did not check it today), that is under $0.01.
- Topic page [dc_55z71al37g](../../wiki/2026-11/2026-11-04-self-host-image-gr-q1jrelx2ty-z71al37g.md) has been rewritten with these results.

## What I need from you
Mitchell: destroy the empty app with `fly apps destroy muster-town-selfhost` (the deploy token cannot), and revoke FLY_SELFHOST_TOKEN.
