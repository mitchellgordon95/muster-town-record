---
id: "dc_cgdu740k3s"
type: "report"
state: "building"
title: "gr_6qlj35wnh3 funded: step 1 (throwaway mode) is already live with tests; step 2 (Bank secrets encrypted) queued as as_giuckzof7x, step 3 (tokens hashed) queued behind it as as_r29k7h6qzi"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_l21uyyu782","dc_ts7ulpuk5o","dc_cl8oesij58"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grant gr_6qlj35wnh3 cut into three steps: step 1 live (#239), step 2 as_giuckzof7x running, step 3 as_r29k7h6qzi waiting on it. Nothing more to queue."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T02:06:36.071Z"
sessionId: "se_5d4l8w5mw6"
assignmentId: "as_2973q6a14i"
costUsd: 1.8685674500000002
tokens: 93428
turns: 14
createdAt: "2026-11-01T02:06:14.159Z"
updatedAt: "2026-11-01T02:06:36.071Z"
---
## What I did
Read the grant plan, the finding [dc_l21uyyu782](../../note/2026-11/2026-11-01-findings-every-copy-of-town-db-carries-the-town-s-1uyyu782.md) and the "Secrets and tokens" page, then checked main (af85f2a) for what #239 already covers and where steps 2 and 3 touch the code. Cut the plan into three steps, one per key result, and queued the two that remain. Rewrote [dc_ts7ulpuk5o](../../wiki/2026-10/2026-10-29-secrets-and-tokens-7ulpuk5o.md) and my Notes page.

## Findings
- **Step 1 (kr_zz0nm8ets4) is done in code.** PR #239 (7ca64bc, live since 02:02 UTC) ships `MUSTER_TOWN_RUNTIME=off`: no startRuntime, restore-only backup job, health `throwaway: true`, and the exact log line the key result names ("[server] runtime off (throwaway)…"), with unit tests in packages/server/test/backup.test.ts. The only evidence left is the next drill's log, which comes from outbox request [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) (Mitchell runs it) and is checked by the existing schedule sc_qz1bojtwyy on 11-02 01:20 UTC. Nothing new queued for it.
- **Step 2 (kr_fbmcxyzot1) → as_giuckzof7x**, building queue, lane grant, pages [dc_ts7ulpuk5o](../../wiki/2026-10/2026-10-29-secrets-and-tokens-7ulpuk5o.md) + [dc_e9s5nh8x7u](../../wiki/2026-10/2026-10-29-prod-working-rules-s5nh8x7u.md). Storage-only change: the two secret-column store classes (users.apiKey, bank_inputs.apiKey in core/src/store.ts) encrypt on write and decrypt on read with the existing encryptSecret/decryptSecret (AAD = table:id), boot back-fill of plaintext rows, wrong key reads null without throwing into fundingFor, no key refuses to store, core tests, docs/secrets.md, PR, merge, live check (sessions keep running, backup.error null). The brief carries the grant's stop condition: pivot and report if token accounting would have to change. Migration numbering: 078 is the highest on main right now.
- **Step 3 (kr_9qpk2gnwa9) → as_r29k7h6qzi**, same lane and pages, waits on step 2 so the migrations don't collide. sha256 of tokens.token in place by migration, resolve hashes the input (no forced logout), per-session tokens for the getOrCreate callers (desk and host sessions, adminToken, seed) revoked at session end, tests, docs, PR, merge, live check (no 401 burst in /api/events, desks keep working).
- After step 3's live check and the drill log: close_grant with the three checks as evidence, then a rollup.
- Budget: the grant has 400,000 tokens; this session plus two build-and-ship sessions should fit, with the drill evidence costing nothing extra.

## What I need from you
Nothing needed.
