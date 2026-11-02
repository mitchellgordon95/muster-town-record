---
id: "dc_57jidmp9ks"
type: "note"
state: "building"
title: "Draft grant: the stranger path (homepage of collectives, open one, sign in, see others live). Ready to file the moment the Onboarding key result exists"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["grant-draft","stranger-path","onboarding"]
createdAt: "2026-10-26T15:17:46.289Z"
updatedAt: "2026-10-26T15:17:46.289Z"
---
# Draft grant: the stranger path

Town hall decision 4 (2026-10-26, mt_a9qzu4swja): once Mitchell writes the Onboarding key result ("A stranger lands on a homepage listing multiple collectives, opens one, signs in, and sees other people live"), Kelly proposes a grant on it. At 15:16Z `GET /api/buildings/bl_hzjw0z0zlz/key-results` is still `[]`, so this note holds the proposal verbatim; the continuation files it with `propose_grant` in one call.

## What the live site does today (checked 2026-10-26, live commit 119bd70)

What the code and the server say:
- **One collective per server.** muster.town serves the `collectives/workshop` collective at `/`; `collective.json` + `.env` configure exactly one. There is no page anywhere that lists collectives, and no registry of them. README: each collective on its own port needs its own GitHub OAuth app (one callback URL per app) unless they share one `MUSTER_TOWN_PUBLIC_URL`.
- **Opening and viewing works as a guest.** Every GET route except `/api/me`, threads and the bank is public; the web client opens in read-only guest mode with a local-only ghost (`web/src/auth/auth.tsx`).
- **Sign-in exists and is configured live.** `GET /api/auth/config` on muster.town returns a GitHub client id and `publicUrl: https://muster.town`. Flow: `/auth/github` → callback → session cookie (30 days) → redirect `/`. A new login becomes a `visitor` user; allowlisted logins get `admin`.
- **Multiplayer is built but not verified with two strangers.** On the first WS auth every user gets an avatar agent of kind `human` at the plaza (`ws.ts`, `ops.ensureAvatar`); `human.move` / `human.say` go over the socket; the renderer draws every agent except your own avatar (`map/renderer.ts:313`). Guests' ghosts are local-only by design, so two guests never see each other.

What I infer: steps 2 and 3 of the key result probably already pass and need a live check with a second GitHub account; step 4 probably passes for two signed-in users and needs the same check; step 1 (a homepage listing multiple collectives) does not exist and is the build.

What I don't know: whether Mitchell wants a second real collective (a second Fly app + OAuth app) or a landing page that lists the workshop collective plus placeholders; whether anyone other than Mitchell has ever signed in to muster.town.

## The proposal (propose_grant fields)

- **keyResultId:** the Onboarding key result once it exists.
- **objective:** A stranger reaches a homepage listing the collectives, opens one, signs in with GitHub, and sees another person moving live on the map, verified on muster.town with a second GitHub account.
- **approach:** (1) A collective registry (a `collectives.json` list of `{slug, name, tagline, url}` the server reads, exposed as `GET /api/collectives`) and a landing page at the root (or `/collectives`, decided with Mitchell) listing them with name, tagline, goal and an "Open" link; the running collective's client moves behind "Open". (2) A second collective entry so the list is real: either a second Fly app with its own `.env` (Mitchell's call; needs a GitHub OAuth app or a shared `MUSTER_TOKEN_PUBLIC_URL`) or a documented placeholder with a link. (3) Guest card and sign-in: the first screen a stranger sees says what the place is and offers Sign in with GitHub; fix anything that breaks on a fresh account (visitor role, avatar at the plaza, the How-this-works overlay). (4) Multiplayer: two signed-in users in two browsers see each other move and `say`; fix what doesn't. Each step ships as its own PR to main with a Craig live check before the next.
- **stopCondition:** All five testing-plan checks pass live on muster.town, or 25 M tokens are spent, or Mitchell cuts the grant. Scaling, a multi-collective server, and custom domains per collective are out of scope.
- **askTokens:** 25,000,000 (my feature PRs ran 1.2–2.5 M tokens each and Craig's live checks ~1.4 M; four build steps + four live checks + one checkpoint ≈ 16 M, with margin).
- **testingPlan:**
  1. Homepage lists at least two collectives with name and tagline. Check: open muster.town in a private window; two entries render; `GET /api/collectives` returns them.
  2. Open a collective and view it without signing in. Check: click Open; the town map, boards and library load read-only in the private window.
  3. Sign in works for a new GitHub account. Check: Sign in with GitHub from the guest card with an account that has never signed in; `/api/me` returns the user with role visitor and an avatar at the plaza.
  4. Multiplayer: another person is visible live. Check: two browsers signed in as two users; each sees the other's avatar move within 2 s and sees a `say` bubble.
  5. Nothing regresses for Mitchell. Check: his admin session still opens the Town Hall in-tray and planning desk after the landing page lands.
- **note for Mitchell:** The one decision the grant needs from you early: do you want a second real collective (a second Fly app and a second GitHub OAuth app, or one shared public URL) or is a listed placeholder enough for now? Everything else is agent work. Checkpoint at 50 %.

