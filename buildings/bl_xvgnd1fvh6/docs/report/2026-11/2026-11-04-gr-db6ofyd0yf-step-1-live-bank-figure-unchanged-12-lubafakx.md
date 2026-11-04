---
id: "dc_nelubafakx"
type: "report"
state: "building"
title: "gr_db6ofyd0yf step 1 live: Bank figure unchanged (124,404), streams phase 32–43 → ~1.3 ms, live tick median 148 → 132 ms (target < 110 needs steps 2–3)"
authorId: "ag_75t860ns84"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 live and checked: Bank figure unchanged (124,404), streams phase 32–43 → ~1.3 ms, median tick 148 → 132 ms. Steps 2 (as_qizum6vt19) and 3 carry the rest of kr_0cbw6jb2p8."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T16:35:38.719Z"
sessionId: "se_h101a55r9e"
assignmentId: "as_gsppk54446"
costUsd: 0.42094889999999996
tokens: 21047
turns: 7
createdAt: "2026-11-04T16:35:25.052Z"
updatedAt: "2026-11-04T16:35:38.719Z"
---
## What I did
- Checked that acf73450 (PR #302, https://github.com/mitchellgordon95/muster-town/pull/302) is live. /api/health reports commit acf73450, and the server booted at 16:30:48Z.
- Read `expectedSessionTokens` from /api/bank/streams twice: at 16:31Z and at 16:35Z.
- Took two sets of 12 /api/health tick samples, 10 s apart: 16:31:09–16:32:59Z and 16:33:04–16:34:59Z.
- Rewrote topic page [dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md).

## Findings
- **The Bank figure did not move.** `expectedSessionTokens` was 124,404 before the deploy (948 samples) and is 124,404 after it (949 samples) at both readings. This holds the live part of kr_2djaq46ga6 for step 1.
- **Live tick, before vs after:**

| | median tick | streams phase |
|---|---|---|
| Before (a84ed22, 16:15Z) | 148 ms (137–163) | 31.8–42.6 ms |
| After, 0–2 min after boot | 141.5 ms (116–165) | 1.1–1.5 ms |
| After, 2–4 min after boot | **131.5 ms** (116–181) | **1.1–1.6 ms** |

- The 11-03 baseline was a median of 199 ms with streams at 29–36 ms.
- In all 24 samples, `error` was null and lagMs was 1–120 ms (one spike at 120).
- **kr_0cbw6jb2p8:** the streams part (< 10 ms) is met. The median part (< 110 ms) is not; it is about 22 ms short.
- **Live time now goes to two phases:**
  - **work, 51–66 ms:** spawnForks/forkableQueue, which runs Bank.debited once per credit. Step 2 (as_qizum6vt19, the GROUP BY) targets this. On the desk after-profile it was 55 % of the tick, so step 2 is still worth doing.
  - **explore, 35–53 ms:** freeTokensAll plus exploreBlock. Step 3 targets this.
- On the desk the tick fell 48 %; live it fell about 11 %. On the desk, streams was half the tick; live it was only 32–43 ms of 148 ms. So steps 2 and 3 carry most of the remaining live cut.

## What I need from you
Nothing needed.
