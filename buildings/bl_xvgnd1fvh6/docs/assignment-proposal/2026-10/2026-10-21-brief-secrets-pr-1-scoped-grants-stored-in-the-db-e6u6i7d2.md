---
id: "dc_6xe6u6i7d2"
type: "assignment-proposal"
state: "building"
title: "Brief: Secrets PR 1, scoped grants stored in the DB and managed at the Town Hall (for Dara)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_8hdfo4rucp","dc_ios62uyco3","dc_ypqynf36zy"],"urls":[]}
tags: ["secrets","prod","assignment"]
createdAt: "2026-10-21T20:58:44.670Z"
updatedAt: "2026-10-21T20:58:44.670Z"
---
Author: Cleo, 2026-10-21. For @Dara. Mitchell approved the host/collective split ([dc_8hdfo4rucp](../../note/2026-10/2026-10-21-secrets-which-belong-to-muster-town-the-host-and-w-dfo4rucp.md), building on Dara's design [dc_ios62uyco3](../../article/2026-10/2026-10-21-design-secrets-for-muster-town-today-on-the-macboo-s62uyco3.md)). Ship PR 1 from that design, with one change from 3a: grants and collective secret values live in the DB and a collective admin manages them at the Town Hall. They do NOT go in `collective.json`.

## Scope
1. **Collective secrets in the DB.** A new table with the name, the value encrypted with AES-256-GCM under the host secret `MUSTER_TOWN_DATA_KEY` (never stored in the DB), and grants (buildings / agents / skills). If the data key is missing, refuse to store values and say so clearly. Never fall back to plaintext.
2. **Admin API, write-only for values:** set or replace a value, delete it, edit grants. The list returns names, grants and set/missing, never values. Collective admins only.
3. **Town Hall panel** for those admins: names, grants, set/missing, and a write-only value input.
4. **`deskEnv()` injects a secret only when it's granted** to the session's building or agent, or to a skill pinned for that agent. Log a `secret.granted {name, sessionId}` event with no value. `DESK_ENV_*` from the host env becomes a localhost fallback: it's injected with a warning for one release, then dropped.
5. **Host secrets never reach a desk.** Host sessions (`runtime/src/sdk.ts`) get an allowlisted env instead of `{...process.env}`. The server stops printing the admin token on start (`server/src/main.ts`): it writes it to `<dataDir>/admin-token` (0600) and prints the path.

Split this into 2 PRs if that keeps them small (e.g. backend + API first, panel second). Push to main per the Prod rules, run typecheck and tests, and queue a redeploy when it lands.

**Why it's urgent:** it must land before we cut the Mac town over to muster.town, because after cutover the Prod building's own agents run on that box.

**Done means:** it's live, and the report explains how to grant `MINICLAW_WS_TOKEN` to the talk-to-wright skill from the panel.
