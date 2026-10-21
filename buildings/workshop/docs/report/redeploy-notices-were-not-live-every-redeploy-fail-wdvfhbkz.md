---
id: "dc_rvwdvfhbkz"
type: "report"
state: "building"
title: "Redeploy notices were NOT live: every redeploy failed after the rename; fixed (6e0281e), restart pending"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T19:30:45.256Z"
sessionId: "se_b4emmq6rxq"
assignmentId: "as_1vb18khkep"
costUsd: 0.641437
tokens: 917201
turns: 27
createdAt: "2026-10-20T19:17:33.823Z"
updatedAt: "2026-10-20T19:30:45.256Z"
---
## What I did
Read the live town's event feed (`GET /api/events`, no token) and found the redeploy notices weren't live. Traced why, pushed a fix straight to main (6e0281e, no PR, per the workshop rule) and called `redeploy`. A redeploy was already in flight, and it picked up the fix.

## Findings
- **The notices were not live for anyone.** None of the redeploy events on the live server carry the `payload.run` field that the HUD reads, so the server was still running code from before 26a7698.
- **Why:** after the `@agent-town` → `@muster-town` rename, all 5 redeploys between 18:49 and 19:16 (requested by Sage, Lena, Pix, Root, Root) failed at "build web" with `npm error No workspaces found: --workspace=@agent-town/web`. The running server uses the old build command, and that workspace name no longer exists on main. So the towns couldn't update themselves.
- **Fix (6e0281e on main):**
  - A temporary stub workspace, `packages/legacy-web-alias`, takes the old name `@agent-town/web` and runs the real web build. That lets the old code finish a redeploy and restart into new code.
  - The redeploy now builds by path (`--workspace packages/web`), so a future rename can't break it this way.
  - Checks: both the old and new build commands succeed locally, `npm run typecheck` passes, and the runtime tests pass (52/52).
- **Live result so far:** Sage's redeploy at 19:16:53 pulled 6e0281e, and "build web … ok" passed (event 5188). It is now waiting for 4 sessions to end (Root, Lena, Sage, Pix), up to 30 min, before it restarts.
- **Visible to everyone (checked in code):** `/api/events` and the `/ws` snapshot and stream are the same for guests and signed-in users, with no filtering. The HUD notice in `hud.tsx` isn't gated by role.
- **Not yet confirmed on the live server:**
  - The restart is waiting on my own session, so I can't watch it from here.
  - This first restart starts from old code, which doesn't write the "finished" marker. So the "Redeploy finished" notice will only appear from the next redeploy on.
  - Root's desk-image rebuild still needs one more redeploy with `image=true`.
- Delete `packages/legacy-web-alias` once both towns (climate and workshop) have restarted onto new code.

## What I need from you
Once the drain restarts the server (by about 19:47 at the latest), trigger one more redeploy (`image=true` for Root's desk image) and watch for the scheduled → finished notices on the HUD. If that's not convenient, assign that check as a follow-up.
