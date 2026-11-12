---
id: "dc_t5ru1yhb9a"
type: "report"
state: "building"
title: "UptimeRobot plan for a fresh uptime grant: Mitchell's clicks, remove the probe path, 3 steps"
authorId: "ag_jqqxa2bn3e"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["mt_msnjkpgwdb","dc_3xcwuz1kn3","dc_boc7bkbhzw","dc_ow4k1e1z1q","dc_z5kbis28sp"],"urls":["https://uptimerobot.com/pricing","https://uptimerobot.com/api/","https://uptimerobot.com/api/legacy/"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. Filed as a fresh proposal continuing gr_rcj8nkbkbt (S remove the probe path, M the server reads UptimeRobot getMonitors behind a 5-min cache, S live check after a real deploy). The key goes in as a Town Hall secret UPTIMEROBOT_API_KEY (world.secrets.value, as FLY_DESKS_ACCESS_TOKEN does, packages/runtime/src/index.ts:806), never through chat; the status page URL as UPTIMEROBOT_STATUS_URL the same way. Mitchell's clicks go out as an outbox request. Rolled up in #47."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-12T14:41:40.026Z"
sessionId: "se_wkj89k2rls"
assignmentId: "as_oq9y3yuerj"
costUsd: 0.6485251
tokens: 32426
turns: 3
createdAt: "2026-11-12T14:40:21.297Z"
updatedAt: "2026-11-12T14:41:40.026Z"
---
## What I did
- Deleted the dropped local branch `agent/cleo-1/gr-rcj8nkbkbt-replan-a-scheduled-github-`. It was never pushed and nothing was committed.
- Stopped the mock server (pid 1028) and removed `/tmp/mock`.
- Read UptimeRobot's pricing page and API pages.
- Mapped the uptime code currently on main.
- Rewrote the topic page [Public uptime](../../wiki/2026-11/2026-11-10-public-uptime-kbis28sp.md).
- Built nothing: every code step needs the URL or the key, or is a removal for a grant to fund.

## Findings
**(a) UptimeRobot free plan: what Mitchell does once, and what he sends**

Limits, from https://uptimerobot.com/pricing (read 2026-11-12):
- "50 monitors" and "5 min. monitoring interval".
- 1 status page ("Basic status pages"). The "Own domain" row has no Free mark.
- "3 months" data retention.
- SMS is "Not included, can be added" (paid credits).
- "Good for personal and commercial projects."

API, from https://uptimerobot.com/api/ and https://uptimerobot.com/api/legacy/:
- The FAQ says the API "is included across all plans, from Free to Enterprise".
- The free limit is "10 req/min".
- A "read-only api_key" can call every get* endpoint.
- "CORS headers are sent only for get* API endpoints with monitor-specific and read-only API keys."
- getMonitors takes `custom_uptime_ranges`.

Not verified:
- The pricing table's checkmarks are images. Whether free email alerts and the API show as included there is inferred, not read.
- Whether the newer v3 API keys work like the legacy read-only key.

Mitchell's steps, about 6 screens:
1. Sign up at uptimerobot.com and verify his email.
2. Add New Monitor → HTTP(s) → `https://muster.town/api/health`, every 5 min, alert to his email. One process serves the Workshop and every hosted collective, so one monitor covers all of them.
3. Status Pages → New → pick that monitor → save, then copy its public URL.
4. Integrations & API → create a **Read-only API key**.
5. Send us both: the status page URL and the read-only key. The key is low risk: it only reads data the status page already shows publicly. It goes in as a server secret, `UPTIMEROBOT_API_KEY`.

Caveat: at a 5-minute interval, most of our restarts (seconds long) won't register as downtime. The block keeps showing restart gaps from the server's own events (`uptime.ts` `restarts()`, line ~120), which is honest about that.

**(b) Probe API, prober role, Pinger posting: recommend REMOVE**

What exists today:
- Ingest: `packages/server/src/routes/uptime.ts:12-15` (POST) and `uptime.ts:20-29` plus the ingest at ~60-70.
- Role: `core/src/migrate-roles.ts:66-68` creates `role:prober`, and `schema/src/index.ts:264,291` adds `town.uptime`.
- Pinger: `deploy/pinger/muster_pinger.py:15-18,47,91-117` (buffer and post).
- Tests: `test/uptime.test.ts` (126 lines) and `test_muster_pinger.py` (83 lines).

Costs of each option:
- **Remove:** roughly −250 to −300 lines. Migration 108's empty `uptime_probes` table stays, since migrations are additive. A one-line migration deletes the unheld `role:prober` row. Knip risk is low because `ProbeBatch` goes with its only user. Pinger SMS alerting (objective ob_648ua06ht0) is kept; only its posting goes.
- **Dormant:** costs nothing now, but leaves a POST endpoint and a role nobody may use, and docs that say the opposite of Mitchell's decision. `home.ts:120` already falsely says "Measured from outside once a minute".

The step that changes the data source rewrites `uptime.ts` anyway, so removing the probe path there costs little extra.

**(c) Plan for a fresh grant** (gr_rcj8nkbkbt was cut, [dc_boc7bkbhzw](2026-11-12-grant-gr-rcj8nkbkbt-cut-c7bkbhzw.md))

Smallest change to the block: keep `Uptime.tsx` and its `/api/uptime` fetch (`Uptime.tsx:24`; used by `BankPanel.tsx:93` and `home/main.tsx:48`). The server's `GET /api/uptime` calls UptimeRobot getMonitors with 30 one-day `custom_uptime_ranges` plus a 30-day total, caches for 5 min (well under 10 req/min), and keeps the restart gaps. The block adds a source line and a link to the status page.

This is better than embedding the status page (an iframe on a page we don't control) or calling UptimeRobot from the browser (puts the key in the page; it would work with CORS but can't be cached). Linking only, with no key, is a fallback if Mitchell sends just the URL: an S change in `Uptime.tsx` and `home.ts:120`.

Key results:
1. **The block shows UptimeRobot's numbers.** The landing and Bank › Hosting › Uptime show UptimeRobot's 30-day uptime % and day strip for muster.town, with a link to its public status page.
   - Check: open muster.town signed out (Skip the tour) and Bank › Hosting. The % matches the status page's 30-day figure within 0.1 points, and the link opens it.
   - Due: 2026-11-17.
2. **No town agent or role measures uptime.** `POST /api/uptime/probes` is gone, role `prober` and `town.uptime` are removed, and `deploy/pinger` only alerts.
   - Check: `curl -X POST https://muster.town/api/uptime/probes` returns 404. `git grep town.uptime` on main is empty.
   - Due: 2026-11-15.
3. **The numbers hold up through a real deploy.** After the next real deploy, `/api/uptime` still answers from UptimeRobot with no error, and the restart shows in the block's restart list.
   - Check: `GET /api/uptime` shows source `uptimerobot`, a non-null pct and the new restart gap.
   - Due: 2026-11-18.

Steps:
1. **S, no key needed, can start now:** remove the probe ingest, prober role (plus a migration deleting the row), `town.uptime`, and the Pinger's posting. Fix the `home.ts:120` text and the deploy/README "VPS pinger" section.
2. **M, needs the read-only key (as a server secret) and the status page URL:** server reads getMonitors with a 5-min cache. Map 30 daily ranges into the current `UptimeSummary` shape, keeping restarts. Add a source line and status page link to the block. Add tests with a mocked fetch.
3. **S, waits for step 2 to be live:** live check after a real deploy, with screenshots (KR 3).

Ask: S + M + S from the table.

## What I need from you
Decide whether to file this as a fresh grant. If yes, ask Mitchell for the status page URL and a read-only UptimeRobot API key (step 2 can't start without them).
