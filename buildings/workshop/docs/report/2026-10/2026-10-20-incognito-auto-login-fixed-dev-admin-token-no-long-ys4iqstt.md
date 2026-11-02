---
id: "dc_u7ys4iqstt"
type: "report"
state: "building"
title: "Incognito auto-login fixed: dev admin token no longer served by npm start"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T21:18:22.122Z"
sessionId: "se_a8algcjvap"
assignmentId: "as_1jr20y1l3e"
costUsd: 0.6761613
tokens: 34249
turns: 25
createdAt: "2026-10-20T20:55:45.628Z"
updatedAt: "2026-10-20T21:18:22.122Z"
---
## What I did
I traced why a fresh incognito browser was being signed in. Then I fixed it and pushed straight to main (206febe, 65eee61). Typecheck passes and the server tests pass (55/55, including a new one). I asked for a redeploy, but it isn't live yet: the server still reports 5a9f291. This session is parked until the deploy lands so I can check it on the live server.

## Findings
- **Cause:** `main.ts` turned dev mode on whenever `NODE_ENV !== "production"`. `npm start` / `scripts/serve.sh` never set `NODE_ENV`, so the live town ran with dev=true.
  - In dev mode, `GET /api/dev/admin-token` gives the admin token to anyone who asks.
  - The web client (`app.tsx` boot) calls it whenever no token is stored, then saves the token to localStorage.
  - So every fresh browser was silently signed in as admin: incognito, and any stranger who could reach the URL. Cookies weren't involved.
- **Fix:**
  - Dev mode is now opt-in: it needs `MUSTER_TOWN_DEV=1`, which `npm run dev` sets and `npm start` doesn't.
  - Defence in depth: the route also returns 403 unless the request is direct from loopback. It refuses requests carrying `X-Forwarded-For`, `Forwarded`, `X-Real-IP` or `CF-Connecting-IP`, which a proxy or tunnel adds.
  - New test in `packages/server/test/rest.test.ts`. README, `docs/architecture.md` and `docs/log.md` are updated.
- **Side effects:** Mitchell's normal browser keeps working because its token is already stored. Without GitHub login configured, a new browser now loads as a guest and has to use "Paste a token" (`<collective>/data/admin-token`).
- **Residual risk:** every browser that visited before this fix still has the admin token in localStorage. Nothing in this change revokes it.

## What I need from you
If the town URL was ever reachable by other people, rotate the admin token.
