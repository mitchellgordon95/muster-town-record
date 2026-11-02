---
id: "dc_nwcbe7srkf"
type: "report"
state: "building"
title: "Workshop rollup 13 (checkpoint, gr_iq5m7dug56 at 100%): Bank steps 1–4 live on cf9267f in adjusted output tokens, drift 1.005 on 22 calibrated sessions; grant now 1,512,728 / 1,666,667 adj. (91%); step 5 needs ~2.0M adj. and your confirmation of the converted subscription inputs"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_t5bo61qeqv","dc_w8ibo8rl1z","dc_92f92zu1o6","dc_r37jd1g124","dc_tl6qpuc0oy","dc_t7pggn295j","dc_tybdq79pr3","dc_9z9kqo7tyc","dc_1laow6beu4","dc_px9lf26w37","dc_s0tl8ffwbl","dc_hf0qpwzx79","dc_3gjht3byon","dc_wftvisgziu","dc_tkb0gbupy9","dc_ke6lr93jnx","dc_w7zqlh7iia","dc_qa5q26t8h3","dc_r6q1pik77p","dc_59oknk0xl7","dc_8eiid5skyo","dc_cllnpvy6ms","dc_vywz02d84w","dc_uuhpzqk034","dc_75ctipmr46","dc_75s1lot72s"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-27T02:59:11.047Z"
sessionId: "se_2l0un7m7yh"
assignmentId: "as_35yvfic7ar"
costUsd: 2.25143665
tokens: 27299
turns: 18
createdAt: "2026-10-27T00:06:56.943Z"
updatedAt: "2026-10-27T02:59:11.047Z"
---
## Shipped
All live on cf9267f (checked 2026-10-27 00:25Z; `GET /api/health` commit cf9267f, accounting "adjusted").
- **6105e18** Bank step 3 (Lena, [dc_s0tl8ffwbl](2026-10-26-bank-step-3-pushed-to-main-6105e18-the-bank-books-tl8ffwbl.md), live check [dc_w7zqlh7iia](2026-10-26-61932f2-verified-live-each-human-grant-adjust-cont-zqlh7iia.md)): every stored amount is in adjusted output tokens. Migration 037 converted the ledger (bank.converted event, ratio Opus ÷30 / Fable ÷24): grant 50M raw → 1,666,667 adj.; inputs bi_au5kt05vlj 40M/day → 1,333,333 adj./day (weekly cap 9,333,333), bi_foh0utko9b 20M/day → 666,667 adj./day (cap 3,333,333). `/api/health` reports accounting "adjusted".
- **dee89b9** Bank step 4 (Keel, [dc_px9lf26w37](2026-10-26-bank-step-4-drift-job-bank-cap-pushed-to-main-as-d-9lf26w37.md), live check [dc_qa5q26t8h3](2026-10-26-dee89b9-is-live-and-the-drift-job-ran-desk-session-5q26t8h3.md)): nightly drift job + bank.cap. First real run 00:00:03Z for 10-26: Fable ratio 1.005 over 22 calibrated sessions (87 back-filled sessions excluded), Sonnet 1.000 (n=3), Opus no calibrated sessions yet. Within the ±10% target.
- **ff19540** directed lane (Lena, [dc_tkb0gbupy9](2026-10-26-human-directed-lane-pushed-to-main-ff19540-directe-b0gbupy9.md)): work a human asked for runs on its own meter ("Directed today"), never held by the exploration allowance; assign/review/meeting decisions take lane "directed" with the human source.
- **73af19e** hover-card title wrap (Keel, [dc_wftvisgziu](2026-10-26-blocked-badge-ui-checked-live-badge-hover-card-cli-tvisgziu.md)); **077a0bd** in-tray flag count (Root, [dc_ke6lr93jnx](2026-10-26-077a0bd-is-live-the-in-tray-header-shows-a-separat-6lr93jnx.md)); **cf9267f** records who ended a meeting (Keel, [dc_cllnpvy6ms](2026-10-27-standup-mt-h9xvyaiwdu-was-ended-by-the-web-end-mee-lnpvy6ms.md): standup mt_h9xvyaiwdu was closed by a human End click, not a bug).
- **7154231** (Root, [dc_8eiid5skyo](2026-10-26-fly-hosts-can-now-push-the-desk-image-themselves-7-iid5skyo.md)): the Fly host pushes the desk image itself on a redeploy with image:true and recreates idle desks. That redeploy is the one waiting on this session; until it lands every desk session arrives raw-only and is back-filled (e.g. se_3rrwhk19cz Opus 376,621 raw → 12,554 adj.), which is why Opus has no calibrated sessions.

## Decided
- Approved: [dc_hf0qpwzx79](2026-10-26-grant-gr-iq5m7dug56-adjusted-40-000-000-tokens-0qpwzx79.md) and [dc_3gjht3byon](2026-10-26-grant-gr-iq5m7dug56-adjusted-50-000-000-tokens-jht3byon.md) (your adjusts 24M → 40M → 50M raw, taken in); [dc_px9lf26w37](2026-10-26-bank-step-4-drift-job-bank-cap-pushed-to-main-as-d-9lf26w37.md), [dc_s0tl8ffwbl](2026-10-26-bank-step-3-pushed-to-main-6105e18-the-bank-books-tl8ffwbl.md) (steps 4 and 3 on main, parked); [dc_tkb0gbupy9](2026-10-26-human-directed-lane-pushed-to-main-ff19540-directe-b0gbupy9.md) (directed lane, parked); [dc_ke6lr93jnx](2026-10-26-077a0bd-is-live-the-in-tray-header-shows-a-separat-6lr93jnx.md) (077a0bd live); [dc_w7zqlh7iia](2026-10-26-61932f2-verified-live-each-human-grant-adjust-cont-zqlh7iia.md) (wake step 3 61932f2 live: a human grant adjust/continue writes one Town row in my in-tray); [dc_qa5q26t8h3](2026-10-26-dee89b9-is-live-and-the-drift-job-ran-desk-session-5q26t8h3.md) (step 4 live, desk image stale); [dc_r6q1pik77p](2026-10-26-bank-step-5-design-done-and-checked-against-the-li-q1pik77p.md) and [dc_75s1lot72s](2026-10-27-bank-step-5-code-read-and-design-pinned-to-files-s-s1lot72s.md) (step 5 design: counter = cap deaths + budget.exhausted deduped by session, real 7-day count 10 + 12 sessions; hold when the subscription's spend is within one median session of the learned cap); [dc_59oknk0xl7](2026-10-26-gr-iq5m7dug56-100-checkpoint-parked-on-the-deploy-oknk0xl7.md) (this checkpoint, parked for the deploy); [dc_8eiid5skyo](2026-10-26-fly-hosts-can-now-push-the-desk-image-themselves-7-iid5skyo.md) and [dc_uuhpzqk034](2026-10-27-redeploy-with-the-desk-image-requested-on-live-715-hpzqk034.md) (7154231, image redeploy requested); [dc_cllnpvy6ms](2026-10-27-standup-mt-h9xvyaiwdu-was-ended-by-the-web-end-mee-lnpvy6ms.md); [dc_vywz02d84w](2026-10-27-mitchell-funded-gr-iq5m7dug56-2026-10-26-16-59z-61-wz02d84w.md) (7154231 live); [dc_75ctipmr46](2026-10-27-wake-steps-1-2-not-started-parked-so-the-waiting-r-ctipmr46.md) (wake steps 1+2 not started, allowance reset so they run).
- Redirected: [dc_wftvisgziu](2026-10-26-blocked-badge-ui-checked-live-badge-hover-card-cli-tvisgziu.md) → Keel as_09rfas2au1 verifies 73af19e live.
- Running now: Lena codes step 5 (as_23e58ae0lf, grant); Root's continuation checks the desk-image push and a fresh desk session's five counters; Keel builds wake steps 1+2 (exploration); Root adds a confirm dialog before "End meeting" (exploration).

## Key results
**kr_vyrhhiyotb — on-track** (checkpoint filed 00:25Z; grant 1,512,728 / 1,666,667 adj. tokens, 91%; the 40,942,090 / 40,000,000 raw in the hold notice converted to this).
How to check vs what the testing plan showed:
- Five counters on a finished session: `GET /api/events` session.ended se_cvv6zfp5fa: input 2,275 + output 9,959 + cacheRead 304,504 + cacheWrite5m 66,758 + cacheWrite1h 0 = 383,496 = raw total; booked 28,186 adj. ✓
- Adjusted everywhere: `/api/health` accounting "adjusted"; Bank page and in-tray amounts in adj. tokens with the five types; a 2M-raw Opus session now books ~67k adj. by the formula (real Opus sessions book raw/30 while back-filled). ✓
- Drift within ±10%: Fable 1.005 (n=22), Sonnet 1.000 (n=3) for 10-26; Opus pending calibrated desk sessions. ✓
- Cap deaths predicted, 7-day counter 0: not yet. No bank.cap since step 4 went live; one budget.exhausted at 22:43Z (Prod's building budget, not a cap). The 7-day zero clock starts when step 5 is live.
- Caveat: real Fable sessions book adjusted ≈ raw ÷13–17, not ÷24/÷30, so the converted subscription inputs probably read about half the real daily allowance; step 4's learned cap (first bank.cap) will show the true size.
Today's spend by lane: exploration 15,357 / 680,952 adj. tokens; directed 18,871 adj. tokens.

## Needs from Mitchell
1. Continue gr_iq5m7dug56 and adjust it to about 2,000,000 adj. tokens: step 5 (build + live check, ~150k) and seven daily verification sessions (~100k) do not fit in the 154k left, so the next 100% hold would stop step 5 mid-way.
2. Confirm or re-enter the two subscription inputs in the new unit: bi_au5kt05vlj 1,333,333 adj./day (cap 9,333,333/week) and bi_foh0utko9b 666,667 adj./day (cap 3,333,333/week). If you want them at the real session ratio instead of ÷30, roughly 2.5M + 1.3M adj./day.
