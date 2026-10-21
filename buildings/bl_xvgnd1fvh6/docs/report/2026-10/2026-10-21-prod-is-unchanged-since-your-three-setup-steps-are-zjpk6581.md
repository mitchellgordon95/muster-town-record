---
id: "dc_wlzjpk6581"
type: "report"
state: "building"
title: "Prod is unchanged since your three setup steps are still pending. I added a tested cutover script, and here is your to-do list"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "add this so i can ssh in and do 1 through 3\nssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICW3ellQhitdwHkkrJPzvDoBao1u1OtHc8laIn/oKXjZ"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T21:41:16.455Z"
sessionId: "se_pwf4eon54x"
assignmentId: "as_fvda2fss02"
costUsd: 0.8165214
tokens: 1043579
turns: 27
createdAt: "2026-10-21T21:07:58.311Z"
updatedAt: "2026-10-21T21:41:16.455Z"
---
## What I did
- Re-read the prod reports and plan ([dc_3dzhz0ljty](2026-10-21-muster-town-is-live-over-https-on-the-prod-box-a-f-zhz0ljty.md), [dc_mltonxkizi](../../article/2026-10/2026-10-21-plan-deploying-muster-town-to-muster-prod-1-and-a-tonxkizi.md)) and checked the box over SSH.
  - None of your three setup steps are done yet: the env file has no token, the `muster` user isn't logged into gh, and CI hasn't been moved.
  - Dara hasn't started PR 1 yet (as_0o8ffll8i6): she has no branch and no PR.
- Wrote `deploy/cutover.sh` and added cutover steps to `deploy/README.md`. Pushed to main as **79478b6**.
- Updated prod to 79478b6 with the box's own redeploy endpoint. `https://muster.town/api/health` now reports commit 79478b6.
- I couldn't queue the Mac redeploy: I still lack `town.redeploy`. The change is only deploy files, so the Mac doesn't need it.

## Findings
- **The cutover is now one command on the box.** `sudo bash deploy/cutover.sh /tmp/town.db` does this:
  - checks the file's integrity;
  - backs up prod's current world to `/var/backups/muster-town/pre-cutover-*.db`;
  - swaps in the new db, restarts, waits for health, and sets maxRunning back to 6.
  - I ran it on the box with a copy of prod's own db. Every step passed, and the slots read `{running:0, max:6}`.
- **The Mac's tokens come along with the db.** The server rewrites `data/admin-token` from the database on every start, so after cutover the Mac's admin token and agent tokens work on prod. Rotate them after cutover.
- **Desk home directories don't migrate.** They live in Docker volumes `deskhome-<agentId>` on the Mac. Notebooks and docs are in the db, so residents only lose local files and checkouts and can re-clone. README step 4 shows how to tar a volume if one is needed.
- **Order to go live:**
  1. Your setup steps.
  2. My smoke test: one resident runs desk → push → PR.
  3. Your SSH key goes in and mine comes out.
  4. Dara's PR 1 lands.
  5. Cutover.
  6. Rotate tokens, then announce.

**Your list, in order:**
1. **Model token and desk env.** SSH to the box. Add `CLAUDE_CODE_OAUTH_TOKEN=…` and the Workshop's `DESK_ENV_*` lines to `/etc/muster-town/env`, but **not** the OVH keys. Then run `sudo systemctl restart muster-town`.
2. **GitHub for desks.** Make a fine-grained PAT covering only agent-town (contents + pull requests). Then run `sudo -u muster -H gh auth login --with-token < pat.txt`.
3. **CI.** Run `git mv deploy/ci.yml .github/workflows/ci.yml` and push. Optionally add an Actions secret `MUSTER_TOWN_DEPLOY_TOKEN` so CI can redeploy. After the first green run creates `prod`, delete the `MUSTER_TOWN_DEPLOY_BRANCH=main` line from the env file.
   - **Tell me when 1–3 are done** and I'll run the smoke test.
4. **SSH key.** Send me your public key, or add it to `~ubuntu/.ssh/authorized_keys` yourself. I'll then remove mine.
5. **Cutover**, once Dara's PR 1 has landed. On the Mac, stop the town, then run `sqlite3 collectives/workshop/data/town.db ".backup /tmp/town.db"` and `scp /tmp/town.db ubuntu@15.204.79.179:/tmp/`. I can run the box side for you.
6. **Before announcing:** create a GitHub OAuth app for muster.town and put `GITHUB_CLIENT_ID`/`GITHUB_CLIENT_SECRET` in the env file. Until then, visitors are read-only guests.

## What I need from you
Do items 1–3 on the list above and tell me when they're done, so I can run the smoke test.

## Reply from Mitchell (2026-10-21 17:41)

add this so i can ssh in and do 1 through 3
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICW3ellQhitdwHkkrJPzvDoBao1u1OtHc8laIn/oKXjZ

