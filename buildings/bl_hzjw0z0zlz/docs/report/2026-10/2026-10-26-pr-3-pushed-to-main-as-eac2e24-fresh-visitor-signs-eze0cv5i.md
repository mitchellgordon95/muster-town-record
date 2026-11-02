---
id: "dc_1jeze0cv5i"
type: "report"
state: "building"
title: "PR 3 pushed to main as eac2e24: fresh visitor signs in as visitor with an avatar; two users see each other move (0.1–0.7 s) and say (0.1–1.1 s); 2 small fixes; redeploy queued, live check parked"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_57jidmp9ks","dc_dj4pdrjn0b"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR 3 eac2e24 approved: fresh-visitor sign-in via the real OAuth path, two-user presence under 2 s, two fixes (no 404/401 on guest load; newcomers spawn on separate tiles). Your parked continuation does the live check when eac2e24 is live; PR 4 (as_tzhxtwc9gh) follows. The real-GitHub checks go to Mitchell in today's rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T18:05:53.697Z"
sessionId: "se_238a1vrkxy"
assignmentId: "as_t20k69hlff"
costUsd: 1.9687807999999996
tokens: 144249
turns: 57
createdAt: "2026-10-26T18:05:02.298Z"
updatedAt: "2026-10-26T18:05:53.697Z"
---
## What I did
- Ran the Workshop locally on a fresh database. A mock GitHub server answered the real `/auth/github` → callback path (it uses the same code as production, which is more than the token login exercises), with two never-seen logins in two headless Chromium profiles.
- Walked each user through: homepage → Open → /workshop/ guest overlay → Sign in → signed in. Then I measured presence between the two.
- Fixed the two problems I found, ran tests (all green), pushed **eac2e24** directly to main (standing rule, so there is no separate PR; branch `agent/craig/pr-3-of-gr-cm3zha6mk6-fresh-visitor-sign`) and queued a redeploy. **eac2e24 should be live after the restart.**

## Findings
**Sign-in path (both users):**
- The homepage shows 2 cards. Open lands on `/workshop/` with the How-this-works overlay. Its last step's "Sign in" goes through GitHub and back to `/workshop/` signed in.
- `/api/me` shows role `visitor` only, `isAdmin:false`, and an avatar of kind `human` at the plaza.
- The overlay doesn't reappear after sign-in.
- The HUD shows only `?`, `▴` and `Sign out`: no admin-only UI.
- No server warnings or errors.

**Fixes:**
1. Every guest load logged a 404 for `/api/dev/admin-token` and a 401 for `/api/me`. `GET /api/auth/config` now also returns `dev` and `session` (packages/server/src/auth/routes.ts:21, schema packages/schema/src/index.ts AuthConfig). The client skips both requests when they would fail (packages/web/src/app.tsx:59 and :70); an older server falls back to the old behaviour. After the fix, both consoles were empty for the whole run. Test: packages/server/test/auth.test.ts.
2. Two newcomers spawned stacked on the same plaza tile, so one hid the other. New human avatars now take the nearest free walkable tile within 3 tiles of the plaza (`freeTileNear`, packages/core/src/entities.ts:238, used at :290). Test: packages/core/test/avatar-spawn.test.ts.

**Presence delay (measured locally, same machine):**
- **Moves:** 7 tile steps were each seen by the other browser 89–721 ms after the client sent them (median about 312 ms). Server receive → broadcast took 2–160 ms. That is well inside the 2 s target.
- **Says:** 3 `say` bubbles appeared on the other screen 83–1124 ms after Enter.
- A key tap under about 250 ms sometimes doesn't cross a tile boundary, so nothing is sent. Movement is pixel-continuous, so that's by design, not a bug.
- On muster.town, network latency adds to these numbers.

**Tests:** typecheck passes; core 268/268, server 73/73, runtime 119/119.

**Screenshots** are in /home/agent/shots/final:
- A/B-1 home
- A/B-2 guest overlay
- A/B-4 signed in, two avatars on separate tiles
- B-5 sees A
- B-6 say bubble
- A/B-3 is only a loading frame: the overlay's last step had already started sign-in.

**Only a real GitHub account can confirm** (about 5 minutes, two accounts or one account plus a private window):
1. On muster.town, Sign in with GitHub using an account that has never signed in. It should land on /workshop/ signed in, and `/api/me` should show `visitor` and an `avatarAgentId`.
2. With two accounts in two browsers, each sees the other walk within about 2 s and sees a typed message (Enter, text, Enter) as a bubble.
3. Mitchell's admin session still opens the Town Hall in-tray and the planning desk.
4. The GitHub OAuth app's callback is still `https://muster.town/auth/github/callback`; PR 1 didn't change it.

**Next session:** live-check eac2e24 on the guest paths (empty console on /workshop/, `/api/auth/config` returns `dev:false, session:false`).

## What I need from you
Nothing needed. The real-GitHub checks above go to Mitchell via the rollup.
