---
id: "dc_zipj6mbjhe"
type: "report"
state: "building"
title: "Prod rollup #46 (gr_8cdix9mpye closed done, 524,619 / 1,500,000): a stranger's box listed a self-hosted town and was delisted when its proof went; public uptime and the redeploy change list are merged and wait on CI's deploy"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_5lovf3z4yq","dc_hcld9cgl7r","dc_g9m8xhzcvl","dc_lyewpwpxw6","dc_v2ujri2o11","dc_b0gspn5uua","dc_e874xhjzth"],"urls":["https://muster.town/api/directory","https://muster.town/api/health","https://github.com/mitchellgordon95/muster-town/pull/418","https://github.com/mitchellgordon95/muster-town/pull/420","https://github.com/mitchellgordon95/muster-town/pull/424"]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "pending"
sessionId: "se_thsqv774od"
createdAt: "2026-11-10T21:46:02.833Z"
updatedAt: "2026-11-10T21:46:02.833Z"
---
Live: 03364d1 since 21:29 UTC (Code Legibility's #417). Prod's three merges today (5409c12d uptime API, 7f12374 redeploy change list, aaa749f3 Uptime block) are on main; CI deploys them at its next window and the live checks are queued on that deploy.

## Shipped

**1. A stranger's box registered a self-hosted town, got listed, and was delisted when its proof went: the directory grant is closed as done**
**What it is:** After your "yes" to Wright, he ran the published image on his VPS and registered it from his box. The well-known proof verified it at 20:18 UTC and it appeared in the public directory as "Self-host proof". He pulled the token; the hourly re-check recorded two misses an hour apart and delisted it by itself before 21:40 UTC, then he tore the town down. I closed gr_8cdix9mpye as done: five key results met, 524,619 of 1,500,000 spent, 975,381 back to the Bank (reports [dc_hcld9cgl7r](2026-11-10-gr-8cdix9mpye-step-3b-phase-2-self-hosted-proof-to-ld9cgl7r.md), [dc_5lovf3z4yq](2026-11-10-gr-8cdix9mpye-step-3b-done-proof-town-delisted-on-ovf3z4yq.md)). One note: the talk-to-wright script prints the MiniClaw WS token in its error line when wss falls back to ws; no Prod fork pasted it anywhere, and the skill ([dc_uvomh0q12e](../../../../../library/skill/2026-10/2026-10-21-talk-to-wright-omh0q12e.md)) is yours to fix.
**What you'd see:** GET https://muster.town/api/directory returns {"towns":[]} again and /api/health shows directory verified 0, listed 0, pending 6. The listing itself is in the report: verifiedAt 2026-11-10T20:18:22Z, name "Self-host proof", host 5.78.179.149.sslip.io. No homepage tile yet: that is Onboarding's, Kelly knows. No picture: the listing lasted an hour and is gone by design.
**Your call:** The grant closed with all five key results met; the proof host was a real VPS rather than the fly.dev app one key result names. Flip that key result to missed on the grant if that matters, otherwise none.

**2. Public uptime: the API and the Uptime block are merged; CI deploys them within the hour**
**What it is:** PR #418 (5409c12d) adds the uptime_probes table, the prober role, POST /api/uptime/probes and the public GET /api/uptime; PR #424 (aaa749f3) adds an Uptime block to the Bank server rack's Hosting tab and the signed-out landing. The VPS pinger buffers its probes and posts them only once it holds a Pinger agent token, so until you make that agent every minute counts as unknown and the block shows no percentage (reports [dc_lyewpwpxw6](2026-11-10-gr-rcj8nkbkbt-step-1-part-1-api-uptime-server-ping-ewpwpxw6.md), [dc_v2ujri2o11](2026-11-10-gr-rcj8nkbkbt-418-brought-up-to-main-and-knip-fixe-ujri2o11.md), [dc_b0gspn5uua](2026-11-10-gr-rcj8nkbkbt-418-merged-5409c12d-424-brought-up-t-gspn5uua.md), [dc_e874xhjzth](2026-11-10-gr-rcj8nkbkbt-424-web-uptime-block-merged-aaa749f3-74xhjzth.md)).
**What you'd see:** Once live: GET https://muster.town/api/uptime returns 30 UTC days of up, down and unknown minutes, a percentage, coverage, outages and restart gaps; the Bank Hosting tab and the landing show an "Uptime" section with 30 day cells. Today all cells are grey and coverage is 0% until the pinger posts. No picture yet: nothing is live.
**Your call:** Once the live commit is at or past aaa749f3, make a visitor agent "Pinger" you own, assign it role:prober, and send Wright its token as MUSTER_PINGER_TOKEN.

**3. The redeploy card will list what went live, with commit links**
**What it is:** Your ask from our 1:1: PR #420 (7f12374) makes each redeploy run record its changes (sha and subject, newest first, up to 50) and the repo URL, so the HUD card lists every merged PR title linking to its commit; "Log" still opens the steps. CI deploys go through the same run, so their cards get the list too (report [dc_g9m8xhzcvl](2026-11-10-redeploy-card-lists-deployed-changes-with-commit-l-m8xhzcvl.md)).
**What you'd see:** The first deploy after 7f12374 is live shows the list on its card; the deploy that carries 7f12374 itself is run by the old code, so that card still shows only the count. A queued check confirms it on the following deploy. No picture yet.
**Your call:** None.

## Decided
- [dc_hcld9cgl7r](2026-11-10-gr-8cdix9mpye-step-3b-phase-2-self-hosted-proof-to-ld9cgl7r.md) → approve (proof town verified and listed; delist continuation queued)
- [dc_5lovf3z4yq](2026-11-10-gr-8cdix9mpye-step-3b-done-proof-town-delisted-on-ovf3z4yq.md) → approve (delisted and torn down; grant closed with this rollup)
- [dc_g9m8xhzcvl](2026-11-10-redeploy-card-lists-deployed-changes-with-commit-l-m8xhzcvl.md) → approve (#420 drafted; the chain merged it as 7f12374)
- [dc_lyewpwpxw6](2026-11-10-gr-rcj8nkbkbt-step-1-part-1-api-uptime-server-ping-ewpwpxw6.md) → approve (#418 drafted: uptime API and pinger buffer)
- [dc_v2ujri2o11](2026-11-10-gr-rcj8nkbkbt-418-brought-up-to-main-and-knip-fixe-ujri2o11.md) → approve (#418 knip-fixed, #424 Uptime block drafted)
- [dc_b0gspn5uua](2026-11-10-gr-rcj8nkbkbt-418-merged-5409c12d-424-brought-up-t-gspn5uua.md) → approve (#418 merged as 5409c12d)
- [dc_e874xhjzth](2026-11-10-gr-rcj8nkbkbt-424-web-uptime-block-merged-aaa749f3-74xhjzth.md) → approve (#424 merged as aaa749f3; live check queued on {deploy: aaa749f3})

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_8cdix9mpye (closed done) | kr_og03nxrkct, kr_a7f8a181a6: register and list shape, no account, no approval | met (close) | 524,619 / 1,500,000; 975,381 returned |
| gr_8cdix9mpye | kr_7c07b8826c: private and Fly-internal hosts never fetched | met ([dc_z92lsjjzdl](2026-11-06-gr-8cdix9mpye-step-3a-live-ssrf-check-passes-on-mu-2lsjjzdl.md)) | |
| gr_8cdix9mpye | kr_89cb8eda84: a stranger-style town is listed | met ([dc_hcld9cgl7r](2026-11-10-gr-8cdix9mpye-step-3b-phase-2-self-hosted-proof-to-ld9cgl7r.md), verifiedAt 20:18:22Z) | |
| gr_8cdix9mpye | kr_dc79c27ff0: delisted when the proof is removed | met ([dc_5lovf3z4yq](2026-11-10-gr-8cdix9mpye-step-3b-done-proof-town-delisted-on-ovf3z4yq.md), towns: [] at 21:40Z) | |
| gr_rcj8nkbkbt (funded) | kr_ay5wb5wfhd: Uptime block on the landing and the Bank server rack | on-track: merged, live check queued | about 252,000 / 260,000 by the four step reports' own figures |
| gr_rcj8nkbkbt | kr_6ofa7wf812: a full day of pinger probes in /api/uptime | not started: needs your Pinger token, then a day | |
| gr_rcj8nkbkbt | kr_nrh9ygog2w: a real restart shows in the uptime figures | not started: needs the live pinger and the next restart | |
| gr_ba0juhlm7n (funded) | hourly off-site backups, restore drill row | backups live; drill row waits on outbox [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) | about 268,000 / 600,000 |

Spend today by lane: exploration 0, directed 114,347 (the redeploy change list); grant lane: gr_8cdix9mpye step 3b and gr_rcj8nkbkbt step 1.

Forecast: the uptime grant will likely reach its 260,000 ceiling on the queued live check and hold. Finishing its last two key results needs your Pinger token, a day of probes and one short check session: adjust it by 100,000, or cut it after the live check and leave two key results unclaimed.

## Needs from Mitchell
1. Once the live commit is at or past aaa749f3: make a visitor agent "Pinger" that you own, assign it role:prober, and send Wright its token as MUSTER_PINGER_TOKEN with a request to rerun step 1 of the VPS pinger install in deploy/README.md. Until then probes only buffer on the VPS and the Uptime block stays grey.
2. The uptime grant will hold at its ceiling after the live check: adjust it by 100,000 so one check session a day after the pinger posts can close it, or cut it then.

_Already waiting in your in-tray: 1 proposal (gr_rdc7hrw4q8), 1 request ([dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 3 rollups ([dc_tzb1f3dbao](2026-11-06-prod-rollup-41-close-report-for-gr-db6ofyd0yf-bank-b1f3dbao.md), [dc_cges6f5hvy](2026-11-09-prod-rollup-43-close-report-for-gr-w9ue1k1p0c-rede-es6f5hvy.md), [dc_d82jxhl3pp](2026-11-10-prod-rollup-45-gr-8cdix9mpye-420-000-1-500-000-the-2jxhl3pp.md))._
