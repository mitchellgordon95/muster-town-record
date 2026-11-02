---
id: "dc_roeig7abhg"
type: "wiki"
state: "building"
title: "Root goal always has a captain (mt_cyd2t5ioob D7)"
authorId: "ag_dsvsu5nj62"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-01T01:59:27.047Z"
updatedAt: "2026-11-01T02:20:45.423Z"
---
State on 2026-11-01 after as_18e5gsfqkx (lane directed, sourceId mt_cyd2t5ioob). DONE.
- **PR #241 = af85f2a LIVE-CHECKED** (GET /api/health 08c16a7 at 02:18:15Z contains af85f2a). Migration 078_root_captain.sql (077 = retainers #238, also on main now).
- Live: GET /api/goals root gl_town ownerId us_1la74k332n (owner name Mitchell). GET /api/buildings/town-hall/intray: all 10 items route to gl_town / Mitchell → his Mine = those 10. Guest goal tree shows root badge "👤 Mitchell" and "Captain: Mitchell"; picture mf_giidd18l6e. Shipped candidate = item 10 on [dc_7lpbltjy1j](../2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).
- What it does: back-fills gl_town.ownerId = earliest admin with a GitHub account, else earliest admin. Goals.ownerOf/route always return a userId; ensureRootCaptain() at boot, seed, admin GitHub sign-in, hub.open. Root captain can be changed, not cleared. "the town admins" fallbacks removed everywhere; root captain requests allowed.
- Admin-only branches that remain (permission, not routing): canFund via building.fund, canEdit via goals.edit, canDecideCaptain via canEdit; in-tray defaultView "all" for admins.
- Reports: [dc_zd2hw4j3u8](../../report/2026-11/2026-11-01-root-goal-always-has-a-captain-pr-241-open-migrati-2hw4j3u8.md), [dc_u5wolcinmb](../../report/2026-11/2026-11-01-pr-241-root-always-has-a-captain-merged-as-af85f2a-wolcinmb.md).
