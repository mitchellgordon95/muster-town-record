---
id: "dc_0zs8zpfwiu"
type: "report"
state: "building"
title: "0fb0b97 live: Talk to Secretary on panel, in-tray header and Town Hall Staff row verified; digest card never rendered (client dropped it), fix PR #321"
authorId: "ag_9l49p3sx8d"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:54:52.355Z"
sessionId: "se_sy8uy8ki31"
assignmentId: "as_lfgphz9is4"
costUsd: 1.6644091
tokens: 83220
turns: 44
createdAt: "2026-11-04T18:34:04.088Z"
updatedAt: "2026-11-04T18:54:52.355Z"
---
## What I did
Read GET /api/health and checked muster.town in headless chromium, as a guest and with a stubbed admin `me` (client-side only; the only non-GET request was the join-funnel view ping). I did not open a 1:1 with the Secretary. While checking, I found that the digest card never shows on the live site. I fixed it in draft PR #321 and parked on its CI.

## Findings
- **Health:** the live commit is `0fb0b97bd5ca35a6ff79e45a8c9ea97c05138b32`, started 18:20:33Z, so it is exactly #308's merge.
- **Secretary agent panel (ag_7tiwyqva83, Talk tab): verified.** It shows its own callout ("Secretary keeps your in-tray digestible… approve a retainer") with a primary **Talk to Secretary** button. The old "works from assignments… Talk to ★ Planner" callout is gone. A guest sees "Sign in to talk to Secretary".
  ![Secretary panel: own callout and Talk to Secretary (live 0fb0b97)](/api/media/mf_ozb5rtl6hn.png)
- **Town Hall in-tray header: verified.** It reads "▶ Review as deck · **Talk to Secretary** · N waiting…".
- **Town Hall building panel, Overview: verified.** The Manager row reads "the root goal's captain: Mitchell. The in-tray is the humans'." The Staff row shows "Talk to Planner" and "Talk to Secretary". The Planner has no ★ in its panel title or its button.
- **Digest card ([dc_0ey523bg2z](../../../../town-hall/docs/digest/2026-11/2026-11-04-digest-2026-11-04-26-decisions-187-rollups-y523bg2z.md)): NOT shown live.** It is also missing on 90212da, so it has never rendered since #305.
  - The server sends `digest` (and `stopped`) on GET /api/buildings/town-hall/intray; I confirmed this in the page's own network response.
  - The web client's `HttpApi.intray` (packages/web/src/api.ts) rebuilt the response field by field and left both out. A React fiber probe showed `TownHallIntray` receiving `digest: null`.
  - Mock mode hides the bug because the mock Api returns the object whole.
  - Effect: no digest card, no Talk to Secretary button on the card, and no "Stopped: for the record" section. That last one also matters for gr_8i952perny's kr_f46tddd9as and the live stop check.
- **Fix:** draft PR https://github.com/mitchellgordon95/muster-town/pull/321.
  - `intrayOf` spreads the server response and fills in defaults for the lists, so `digest` and `stopped` are kept.
  - New test `packages/web/test/intrayOf.test.ts`. The full web suite passes (317/317) and typecheck passes. Web-only, no migration.
  - It doesn't touch the same code as PR #317 (#317 changes DigestCardView; #321 changes api.ts).
- Topic page [dc_t20pm17xh1](../../wiki/2026-11/2026-11-04-the-secretary-gr-kdlogzzo5s-0pm17xh1.md) now marks step 3b "LIVE, verified" and records the bug and #321.
- **Next session:** when #321's CI passes, merge it and redeploy. Then re-run ~/demo/sec308b.mjs (or the same check) to confirm `.digest-card` shows with its Talk to Secretary button.

## What I need from you
Nothing needed. The continuation merges #321 when its CI passes.
