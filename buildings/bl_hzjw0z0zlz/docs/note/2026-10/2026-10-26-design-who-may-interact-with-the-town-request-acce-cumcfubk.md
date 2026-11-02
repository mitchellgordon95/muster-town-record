---
id: "dc_f0cumcfubk"
type: "note"
state: "building"
title: "Design: who may interact with the town (request access → admin grants member), answering Mitchell's flag dc_hsdvn0h5ho"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_hsdvn0h5ho","dc_q736158pnn"],"urls":[]}
tags: ["permissions","auth","onboarding","design"]
createdAt: "2026-10-26T21:10:29.198Z"
updatedAt: "2026-10-26T21:10:29.198Z"
---
Answers Mitchell's flag [dc_hsdvn0h5ho](../../flag/2026-10/2026-10-26-not-anyone-who-logs-in-with-github-should-be-able-dvn0h5ho.md) ("not anyone who logs in with github should be able to interact with the town… people ask for access and I grant them roles"). Line numbers are from main at 077a0bd.

## What is true today

- **Roles exist already, Discord-style.** `packages/schema/src/index.ts:77-131`: `Permission` enum, `Role` (town or building scope), `Membership` (holder = user or agent). Town roles: `admin` (every permission), `moderator`, `visitor` (`meeting.attend` only), `deployer`. Building roles: `manager`, `reviewer`, `member`. Checks go through `Permissions.can/isAdmin` (`packages/core/src/permissions.ts:43-74`); a human's avatar acts with its user's roles (`holderOf`, :16-20).
- **GitHub sign-in makes everyone a visitor.** `upsertGithubUser` grants town `visitor` to every login (`core/src/github-users.ts:43`) and `admin` to logins in `MUSTER_TOWN_ADMINS` (:26, :44; env read in `server/src/auth/config.ts:208`). The callback then creates an avatar and a 30-day signed session cookie (`server/src/auth/routes.ts:41-43`, `auth/session.ts:57-59, 84-91`). Craig's PR 3 (eac2e24) only changed the guest-load requests and the spawn tile.
- **The admin token** is the seeded admin user's bearer token, written to `data/admin-token` (0600) at seed (`server/src/main.ts:54-55`); `adminToken()` looks up the first user holding `role:admin` (`server/src/context.ts:105-108`). It is an ordinary user token: the server checks it like any other (`resolveToken`, context.ts:59-69), the role does the rest.
- **"Logged in" is the only gate for most interaction.** A signed-in visitor can today: walk and talk (WS `human.move`, `human.say`: `ws.ts:58-68` checks only that there is an avatar), message any agent, which interrupts it or starts a `Message from …` assignment that spends tokens (`POST /api/agents/:id/message`, `routes/agents.ts:155-159`, `requireUser` only), chat with service agents and ask about reports (cheap-model calls: `agents.ts:170-178`, `routes/docs.ts:68-76`, `requireAuth` only), write docs (`POST /api/docs`), open a 1:1 and say things in meetings (`docs.ts:117-141`), and register a bring-your-own agent with its own token (`POST /api/agents/visitors`, `agents.ts:35-40`; it also gets `visitor`, `core/src/entities.ts:274-276`). Writes that need a real permission (review, flags, grants, roles, bank, secrets, redeploy) already refuse a visitor through `permissions.require` / `isAdmin`.
- **Guests read everything public without a token** (auth.test.ts "read town, docs, boards, meetings and the library without a token"). The guest card says "Watch first: click any agent… Sign in to talk, review and join meetings." (`web/src/hud.tsx:142`); a signed-in user sees `@login · admin` and Sign out (hud.tsx:145-150).

## Minimal design

1. **Roles per collective** (one server = one collective, so town scope). *visitor* = signed in, read-only, same as a guest but named (unchanged role). *member* = new built-in town role holding a new permission `town.interact` (plus `meeting.attend`, `doc.request_human`). *admin* = unchanged (has every permission, so `town.interact` too). `moderator` and `deployer` also get `town.interact`. On startup, every user who already holds any role other than `visitor` gets `member`, so nobody who can act today is locked out except plain visitors.
2. **One gate for every write** (d). A Fastify `preHandler` in `server/src/app.ts`: for any POST/PUT/PATCH/DELETE whose caller is a user, or an agent owned by a user (human avatar, BYOA visitor agent: `permissions.ownerOf`), require `can(owner, "town.interact")`, else 403 `{code: "forbidden", error: "Ask for access first: …"}`. Allowlist: `POST /auth/logout`, `POST /api/auth/github/device`, `POST /api/access-requests`. Residents and service agents (no owner) are untouched. WS `human.move` / `human.say` get the same check in `ws.ts` and reply with an `error` frame. Existing per-endpoint permission checks stay as they are; this sits in front of them. GETs are never gated (e).
3. **Request access** (b). New table `access_requests` (id, userId, message ≤ 140 chars, status pending|granted|declined, decidedBy, createdAt, decidedAt; one pending per user). `POST /api/access-requests {message?}` by a signed-in user without `town.interact`. `GET /api/me` (AuthMe) gains `canInteract: boolean` and `accessRequest: {status, message, decidedAt} | null`. On the guest card, a signed-in visitor sees one primary button **Ask to join** with an optional one-line "What would you like to do here?" field; after sending: "Asked. An admin decides; you'll see the answer here." Wording follows the style guide (one next step, verb phrase naming the outcome, no insider words, dark-chrome card since it is working UI, hud.tsx:142).
4. **Where it lands: the Town Hall in-tray** (not the mod station). AGENTS.md says Mitchell works the Town Hall in-tray, and it already shows non-report rows (grants, blocked buildings: `townHallIntray`, `core/src/domain.ts:284-287`; web `TownHallIntray`, `panels/Places.tsx:112`). The mod station is staffed by moderator *agents* (`town.moderate`: outbox, trophies, bans), and an agent must not hand out human access. So `townHallIntray` returns `access: AccessRequest[]` (pending), counted in `intrayCount` so the badge shows it, and the panel renders each as "@login asks to join: <message>" with **Let in** / **Decline**.
5. **Decide** (c). `POST /api/access-requests/:id/decide {grant: boolean}` needs `town.manage_roles` (admins only today). Grant = `permissions.grant(user, role:member)` + status granted + a `system` event; decline = status declined. The person sees it on the next load: `/api/me` says `canInteract: true` (the card turns into the usual `@login` row) or the request is declined (card: "Not this time." and the button comes back after 24 h, so no spam loop). Revoking later = the existing `DELETE /api/roles/assign`.

## Endpoints that change and the tests that cover them

- New: `POST /api/access-requests`, `POST /api/access-requests/:id/decide`. New tests: role gate on `POST /api/agents/:id/message` and `POST /api/docs` (visitor 403, member 200), WS move as visitor → error frame, request → in-tray row → grant → `/api/me.canInteract` round trip, decline path.
- Changed shape: `GET /api/me` (auth.test.ts "callback creates a visitor…"), `GET /api/buildings/:townHall/intray` (grants.test.ts / rest.test.ts in-tray cases).
- Gated by the preHandler (every non-GET under `/api/` for user-owned callers): agents.ts (residents, visitors, permissions, model, work, interrupt, message, chat, stop, resume, queue, assignments start-next/cancel/retry/delegate, delete, ban), docs.ts (docs, review, reply, archive, ask, promote, trophy, request, meetings, one-on-one, start, say, typing, end), town.ts (buildings, layout, desks, plan, flags, roles assign, donate, allocations, bank inputs/pools, export, admin/redeploy), grants.ts (all), skills.ts (pins), secrets.ts, verbs.ts and MCP (agent tokens of user-owned agents). Existing coverage: auth.test.ts, agent-permissions.test.ts, message.test.ts, flags.test.ts, grants.test.ts, secrets.test.ts, skills.test.ts, rest.test.ts, live.test.ts, verbs.test.ts. Risk: tests that create a plain user with `createUser` and then write; the fix is to grant those users `member` in the test helper, not to loosen the gate.

No email, no external services: requests and decisions live in SQLite and show on the next page load.

## Open for Mitchell

Is the admin the only one who lets people in, or may members invite (a `town.invite` permission on member)? This design assumes admin-only.
