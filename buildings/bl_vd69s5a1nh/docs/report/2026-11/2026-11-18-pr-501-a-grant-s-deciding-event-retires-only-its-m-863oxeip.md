---
id: "dc_4g863oxeip"
type: "report"
state: "building"
title: "PR #501: a grant's deciding event retires only its money asks; parked on CI"
authorId: "ag_phs2i5250h"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-18T00:11:52.082Z"
sessionId: "se_75tqgcs5gl"
assignmentId: "as_jtrez0o0eh"
costUsd: 0.5395012
tokens: 26975
turns: 15
createdAt: "2026-11-18T00:11:52.076Z"
updatedAt: "2026-11-18T00:11:52.082Z"
---
## What I did
I found Mara 2's uncommitted edits in the desk stash and applied them. One conflict came up in packages/core/src/asks.ts: PR #496 had already removed `needAtForecast`/`retireGateAsk`, so I kept main's side and dropped those stashed hunks. I ran typecheck and the asks tests, then `npm run check --fast`. I committed bb8505d7 and pushed; the pre-push hook passed in 32 s. Then I opened the draft PR https://github.com/mitchellgordon95/muster-town/pull/501.

## Findings
- **Change:** `retireAsks` and `settleNeeds` take an optional ask type (`only`). Three callers pass "money": `onGrantEvent` (fund, continue, adjust, counter, reject, cut, close, withdraw, stopping), retainers.ts `releaseRetainer` and `decideRetainer`. A credential, policy, click, do or meeting card on the same grant or retainer now stays live until its own decision. Callers for other target kinds are unchanged.
- **Cause, from Mara 2's report [dc_yvgkuk2mv1](2026-11-17-live-moved-to-7a886f88-481-485-live-ci-still-401-a-gkuk2mv1.md):** closing gr_eztubyh7nf retired the CI deploy token credential ask ak_tlets696sj before anyone read it. Mara 2's own reading counted 49 asks retired on a grant or retainer deciding event since 2026-11-01. That number is theirs; I did not re-scan.
- **Test:** packages/core/test/asks.test.ts › "a grant's or retainer's deciding event retires only its money asks: a credential or policy card on it stays live ([dc_yvgkuk2mv1](2026-11-17-live-moved-to-7a886f88-481-485-live-ci-still-401-a-gkuk2mv1.md))". The asks suite passes 11/11.
- **Docs:** I added this to invariant 3 in docs/invariants/asks.md, which names the test. I also updated invariant 4 and docs/legible-delegation.md §4 item 3, and added the log entry docs/log.d/2026-11-18-mara-1-finish-a-grant-s-deciding-event-retires.md.
- **check --fast:** typecheck and docs/deadcode pass, and 336 of 337 tests pass. The one failure was packages/server/test/backup.test.ts, a worker-thread timer-gap assertion: 108 ms against a limit of 100 ms. It is a load flake and has nothing to do with this change: the file passes 27/27 when run alone.

## What I need from you
Nothing needed.
