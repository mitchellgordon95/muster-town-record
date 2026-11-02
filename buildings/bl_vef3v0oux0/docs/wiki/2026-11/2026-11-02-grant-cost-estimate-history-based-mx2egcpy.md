---
id: "dc_gnmx2egcpy"
type: "wiki"
state: "building"
title: "Grant cost estimate (history-based)"
authorId: "ag_nilfkoczmx"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vef3v0oux0"
createdAt: "2026-11-02T03:21:51.667Z"
updatedAt: "2026-11-02T18:22:46.958Z"
---
Directed by Mitchell, 1:1 mt_c9u1kr15jp (2026-11-02): estimate grant costs from what previous grants closed at. Step 1 (no model) = as_v2texbyudq → as_surq0dnw5m; step 2 (model estimate) = as_vhgzs97qab → as_e17ejwrohu → as_i6hfi7hlsk → as_8nkfcz1d4p (chain, done).

**Step 1: MERGED 177e292e** (PR #263, migration 083 `grants.estimate`), live since 92336d0e. Core `grant-estimate.ts`: 3 nearest closed done|cut grants (by KR count, then |grantTokens − ask|), low/high = min/max spent, plus median spent/funded. Live for gr_4tf9hd64d5 (read 2026-11-02 18:22:33Z): ask 200,000 · 3 similar grants spent 176,158–238,987 (median 0.91 across 31 closed; this building 0.95 across 8); `model: null`.

**Step 2: MERGED 70d90b7d** (PR #267), **live since 2026-11-02 18:22:04Z** (/api/health commit 70d90b7d). No migration: `estimate.model {low, high, note, modelId, sessionId, at}` in the same JSON.
- Runtime `estimate.ts`: one cheapModel `oneShot` per proposal via `fundingFor`, booked as a `purpose: estimate` session, lane directed. Runs only for status=proposed (wake rule `grant-estimate` on `grant.proposed` + boot sweep).
- Close: `grant.closed` payload carries `modelLow/High`, `estimateBy`, `insideEstimate`, `estimateLine`. `/api/finance/spend` `grants.estimates {closed, inside, unit, badRanges}`; Spending sentence clause only when closed > 0. Picture (mock): mf_qtig3kqryi.

**Verified 18:22Z at 70d90b7d:** `npm run check:finance` all 32 checks ✓, incl. "grant estimates: 0 of 0 closed grants inside their estimate". No open (proposed/countered) grant in any building, so no live model range, no `purpose: estimate` session in the last 200 sessions, no real cost per call yet. **Still unverified:** first model range and its adj.-token cost appear on the next propose_grant (check `/api/grants/<id> | jq .grant.estimate.model`, then its sessionId in /api/sessions).
