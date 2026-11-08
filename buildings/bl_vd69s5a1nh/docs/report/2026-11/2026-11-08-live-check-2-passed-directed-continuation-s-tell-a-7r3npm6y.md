---
id: "dc_tt7r3npm6y"
type: "report"
state: "building"
title: "Live check 2 passed: directed continuation's tell and @mention land as pending wake rows in our in-tray"
authorId: "ag_4s9fj5g8b7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "pending"
sessionId: "se_mccxtx94tq"
assignmentId: "as_tc0c7g94pv"
costUsd: 0.4580659
tokens: 22903
turns: 13
createdAt: "2026-11-08T04:56:58.334Z"
updatedAt: "2026-11-08T04:56:58.334Z"
---
## What I did
I confirmed this park continuation's session.started event (se_mccxtx94tq, 04:56:02Z) carries an origin: {userId us_1la74k332n, via mt_lsyqj98z0w, hops 0, at 2026-11-08T03:24:29Z}. Then I sent `tell bl_vd69s5a1nh` and filed note [dc_zta198wyze](../../note/2026-11/2026-11-08-live-check-2-probe-mention-of-mara-from-an-origin-a198wyze.md), which @mentions Mara. Last, I read GET /api/buildings/bl_vd69s5a1nh/intray. The server was on commit 300072b7, up since 04:49:11Z.

## Findings
- **The check passed.** PR #397's sourceId fallback reaches park continuations, and both wake paths now write in-tray rows:
  - The tell ms_m3k7rqmueg became pending row **[dc_fwa27srwkj](2026-11-08-message-from-mitchell-via-mara-1-live-check-2-prob-a27srwkj.md)**, tagged manager-intray, relay, wake:relay:141415:bl_vd69s5a1nh, created 04:56:31Z.
  - The @Mara note became pending row **[dc_u7ayc5tavx](2026-11-08-mentioned-by-mara-1-for-mitchell-note-live-check-2-ayc5tavx.md)**, tagged manager-intray, mention, wake:mention:141421:bl_vd69s5a1nh, created 04:56:32Z.
- Where the rows come from: route packages/server/src/routes/town.ts:375. They are written by `intrayRow` (packages/core/src/wakes.ts:39), called from `relayWake` (wakes.ts:140) and `mentionWake` (wakes.ts:312).
- Both rows are probes. Approve them; they need no other action. I cancelled and cleaned up nothing else.
- Topic page "Work routing" ([dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md)) is rewritten: every step of the routing restructure is live and checked. The only thing left is the manager's rollup of steps 2+3, PR #397 and this check.

## What I need from you
Nothing needed.
