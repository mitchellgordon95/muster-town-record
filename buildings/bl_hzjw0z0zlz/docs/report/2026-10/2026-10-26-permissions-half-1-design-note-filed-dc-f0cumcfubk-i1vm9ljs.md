---
id: "dc_p6i1vm9ljs"
type: "report"
state: "building"
title: "Permissions half 1: design note filed (dc_f0cumcfubk). Signed-in visitors need a member role to act, ask to join from the guest card, and Mitchell decides in the Town Hall in-tray. Half 2 (code) is next"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_hsdvn0h5ho","dc_f0cumcfubk","dc_q736158pnn"],"urls":[]}
tags: []
verdict: "continue"
decision: "continue"
decisionNote: "Half 2 as proposed: build dc_f0cumcfubk on main. Assume admin-only lets people in (Mitchell's answer on member invites is in my rollup; if he says members may invite, that is a follow-up, not a reason to wait). Keep the gate allowlist exactly as the note lists it; fix tests by granting test users member, never by loosening the gate. Guest-card copy per muster-style-guide dc_q736158pnn. Commit and push to main; no redeploy (I queue it). Report with commit sha, test output and the two VITE_MOCK screenshots. Cap ~3 M tokens; if the build is not green by then, push what passes and report."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T21:24:31.493Z"
sessionId: "se_gedgqwrxnr"
assignmentId: "as_u21aizphep"
costUsd: 1.0648365000000002
tokens: 41741
turns: 25
createdAt: "2026-10-26T21:10:52.256Z"
updatedAt: "2026-10-26T21:24:31.493Z"
---
## What I did
I read the auth and session code, Craig's eac2e24, the admin token path, the roles in schema and core, every write route, ws.ts and the guest card copy. Then I filed the design note [dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md). A redeploy was waiting for my session to end, so I stopped after half 1, as the assignment allows. No code is pushed and nothing new needs to go live.

## Findings
**What is true today** (main 077a0bd):
- Roles already exist: town admin, moderator, visitor and deployer, and building manager, reviewer and member (`schema/src/index.ts:77-131`, `core/src/permissions.ts:43-74`).
- Every GitHub login gets town `visitor` (`core/src/github-users.ts:43`). Logins listed in `MUSTER_TOWN_ADMINS` also get admin (:44).
- The admin token is the seeded admin user's ordinary bearer token, written to `data/admin-token` (`server/src/main.ts:54`, `context.ts:105-108`). Its role is what makes it powerful.
- "Logged in" is the only gate for a lot of interaction:
  - moving and talking over WS (`ws.ts:58-68`)
  - messaging any agent, which starts paid work (`routes/agents.ts:155`)
  - chat and ask (`agents.ts:170`, `docs.ts:68`)
  - writing docs and joining meetings (`docs.ts:44, 117-141`)
  - registering your own agent (`agents.ts:35`)
- Review, flags, grants, roles, the Bank, secrets and redeploy already refuse visitors.

**The design in five lines:**
1. A new town role `member` with a new permission `town.interact`. Admin, moderator and deployer get it too. At startup, every user who already holds a role other than visitor becomes a member.
2. One preHandler in `server/src/app.ts` checks every non-GET from a user, or from an agent a user owns, for `town.interact`. WS move and say get the same check. Reading is never gated.
3. On the guest card, a signed-in visitor gets an **Ask to join** button and an optional one-line message. This sends `POST /api/access-requests` and saves it in a new SQLite table.
4. Requests show in the **Town Hall in-tray**, not at the mod station. Mitchell already works the in-tray and it already shows rows that aren't reports. The mod station is staffed by moderator agents, and an agent shouldn't hand out human access.
5. **Let in** / **Decline** calls `POST /api/access-requests/:id/decide`, which needs `town.manage_roles`. The person sees the answer on their next load through `/api/me.canInteract`.

The note lists the endpoints that change and the existing tests that cover them.

**Shipped:** the note only. No commit.

**Left (next session):** build it on main. That means the migration and table, the gate, the two routes, the AuthMe fields, the in-tray rows and the guest card. Tests: the gate on `POST /api/agents/:id/message`, WS move as a visitor, and the request → in-tray → grant → `/api/me` round trip. Then typecheck, server tests, and screenshots at 1400×900 and 390×844 with VITE_MOCK=1. Main risk: tests that create a plain user and then write will need that user made a member in the helper.

## What I need from you
Mitchell decides: is he the only one who can let people in, or may members invite others too? The design assumes only he can.
