---
id: "dc_o631yrd4s2"
type: "report"
state: "building"
title: "Permissions half 2 on main (db3534a): signed-in visitors are read-only until an admin lets them in; Ask to join on the guest card, Let in / Decline in the Town Hall in-tray"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "db3534a on main matches the design and Mitchell's meeting decision (admin-only, no member invite, kr_pxisdsocdp kept). Redeploy queued this session; you get a post-deploy curl-level live check as a separate assignment. The never-granted-account round trip is Mitchell's (in the rollup)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T22:33:52.627Z"
sessionId: "se_eu39n89i0b"
assignmentId: "as_osmbg88640"
costUsd: 2.8777931
tokens: 222067
turns: 76
createdAt: "2026-10-26T22:22:06.124Z"
updatedAt: "2026-10-26T22:33:52.627Z"
---
## What I did
I built design [dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md) on top of WIP 52fe5cf and pushed it straight to main as **db3534a**, rebased onto dee89b9. I did not redeploy (the manager queues it). After db3534a deploys, `/api/health` should contain db3534a.

## Findings
- **Gate:** one `preHandler` in `server/src/app.ts` covers every non-GET request from a user, a human avatar or a bring-your-own visitor agent. Without `town.interact` the caller gets a 403: "Ask for access first: …". The allowlist is exactly the three routes in the note: `POST /auth/logout`, `POST /api/auth/github/device` and `POST /api/access-requests`. Residents and service agents are not gated. The WebSocket `human.move` and `human.say` messages get the same check and reply with an error frame.
- **Roles:** there is a new town `member` role. Moderator and deployer also hold `town.interact`. `migrateRoles` gives member once to every user who holds any role other than visitor, so nobody who can act today is locked out.
- **Routes:**
  - `POST /api/access-requests` takes an optional message of up to 140 characters. A user can have only one pending request.
  - `POST /api/access-requests/:id/decide {grant}` needs `town.manage_roles`, so only admins can decide, as the note assumes.
  - `/api/me` now includes `canInteract` and `accessRequest`.
  - After a decline, the person can't ask again for 24 h.
- **Town Hall in-tray:** a new "Asking to join" section shows "@login asks to join", their message, and **Let in** / **Decline**. These requests count in the in-tray badge.
- **Guest card:** a signed-in visitor sees "You can watch and read. To talk with agents and join in, ask to join.", a "What would you like to do here? (optional)" field and one primary button, **Ask to join**. After asking it reads "Asked. An admin decides; you'll see the answer here." Their moves and messages stay local until they are let in.
- **Tests:**
  - New `server/test/access.test.ts`, 5/5 pass. It covers: visitor 403 on message, docs and visitor-agent writes; member gets 201; logout allowed; the gate on a visitor's own agent vs a resident; the full round trip (ask, in-tray row and badge +1, a visitor can't decide, Let in, canInteract true, deciding twice is refused); decline and the 24 h wait; WS move error.
  - Server access, agent-permissions, rest and auth: 33/33. Web: 61/61. Core v12 and redeploy pass. Typecheck is clean for core, server and web.
  - I fixed existing tests only by granting member to the test users that write. I also updated the deployer permission list and the v1.1 database fixture to drop the new table.
  - The full-suite runs, done in parallel on my loaded desk, also had a few unrelated tests hit the 5 s vitest timeout (memory log and others). Re-run alone, the ones I checked passed or timed out again.
  - I did not re-run tests after the rebase onto dee89b9, which only touched the Bank code.
- **Screenshots (VITE_MOCK):** the files are in `/home/agent/lcs/perm/`: desk-ask, desk-asked, desk-intray, phone-ask and phone-asked.
  - At 390×844 the guest card shows who is here, then the line, the field and the full-width Ask to join button, with "@guest · Sign out" below.
  - At 1400×900 the Town Hall in-tray shows "ASKING TO JOIN 1: @octocat asks to join 40m ago, 'I'd like to help with the onboarding copy', Let in / Decline" above the manager reports.
  - No page errors in either size.
  - The desk-ask shot itself was taken before the card had rendered (its text read back empty). The desk-asked shot shows the card fine after asking.

## What I need from you
Queue the redeploy for db3534a.
