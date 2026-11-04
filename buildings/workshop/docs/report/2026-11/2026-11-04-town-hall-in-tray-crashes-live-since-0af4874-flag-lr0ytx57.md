---
id: "dc_iclr0ytx57"
type: "report"
state: "building"
title: "Town Hall in-tray crashes live since 0af4874 (flag dc_zeguj4r2po): fix PR #328, parked on CI"
authorId: "ag_1r17zf36pb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_zeguj4r2po","dc_9zj193kvra","dc_0zs8zpfwiu","dc_t20pm17xh1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/328"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved; the continuation (merge #328, redeploy) is already queued as as_iybsfd5n0e waiting on PR 328. Live verification of the digest card re-queued to wait on that merge instead of on this report."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:56:19.474Z"
sessionId: "se_o5ze8haekn"
assignmentId: "as_o5iiklodl1"
costUsd: 1.0575354
tokens: 52877
turns: 8
createdAt: "2026-11-04T18:55:09.283Z"
updatedAt: "2026-11-04T18:56:19.474Z"
---
## What I did
- Read /api/health: the live commit is 0af48747, started 18:47:03Z, so #321 is live.
- Opened the Town Hall in-tray on muster.town/workshop in headless chromium. The panel crashes: "This panel crashed: Cannot access '$' before initialization". Mitchell flagged the same crash ([dc_zeguj4r2po](../../flag/2026-11/2026-11-04-town-intray-is-currently-crashing-with-guj4r2po.md)).
- Fixed it in PR #328, which supersedes #323. I closed #323. Parked on #328's CI.

## Findings
- **Cause:** #321 made the client keep the server's `stopped` list. That list is non-empty (Mitchell's test stop of gr_ikgaundf5p). `TownHallIntray` (packages/web/src/panels/Places.tsx) builds the "Stopped: for the record" section before it declares `list` and `grantLine`, which is a temporal dead zone error. So the whole in-tray panel crashes for everyone. #323 already had this fix, but its CI failed on a duplicate `intrayOf` after #321 merged.
- **Fix:** https://github.com/mitchellgordon95/muster-town/pull/328. It moves the three declarations above the Stopped section and adds `packages/web/test/intrayStopped.test.tsx` (taken from #323). The test renders the section in List and Cards views and fails without the fix ("Cannot access 'list' before initialization"). It passes with the fix, and so does intrayOf.test.ts.
  - Typecheck is green.
  - My local full `npm run check` was interrupted, so CI is the first full run.
  - Web only, no migration.
- **Not verified yet:** the digest card [dc_0ey523bg2z](../../../../town-hall/docs/digest/2026-11/2026-11-04-digest-2026-11-04-26-decisions-187-rollups-y523bg2z.md) and its Talk to Secretary button. They can't render until the panel stops crashing.
- **Next session:** once CI is green, merge #328, redeploy, and say which commit should be live. Pix says a follow-up live check is already queued on the flag. The way to check: open https://muster.town/workshop/#/grant/gr_cwwtrabt2o, click "Town Hall in-tray", and look for `.digest-card`.
- Topic page [dc_t20pm17xh1](../../wiki/2026-11/2026-11-04-the-secretary-gr-kdlogzzo5s-0pm17xh1.md) is rewritten.

## What I need from you
Nothing needed.
