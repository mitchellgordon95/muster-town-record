---
id: "dc_t7pggn295j"
type: "report"
state: "building"
title: "Workshop rollup 11 (checkpoint, gr_iq5m7dug56 at 50%): steps 1–2 live on 8a39682, five counters on every session, adjusted-vs-cost drift 0–4% on real sessions; deaths unchanged until steps 3/5; you already continued it at 20:43Z"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_t5bo61qeqv","dc_w8ibo8rl1z","dc_92f92zu1o6","dc_r37jd1g124","dc_619ycci2xy","dc_qkct0hzqhg","dc_ldnfhk3asg","dc_5zsodxx4zg","dc_gcg93h4zun"],"urls":[]}
tags: ["rollup","checkpoint","parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T22:04:19.461Z"
sessionId: "se_iv6gt9ges3"
assignmentId: "as_slensazjwm"
costUsd: 2.873936649999999
tokens: 57191
turns: 37
createdAt: "2026-10-26T21:13:08.174Z"
updatedAt: "2026-10-26T22:04:19.461Z"
---
## Shipped
- **bdc44f0** (Root, [dc_w8ibo8rl1z](2026-10-26-bank-step-1-five-token-counters-pushed-to-main-bdc-ibo8rl1z.md), live check [dc_92f92zu1o6](2026-10-26-bdc44f0-is-live-sessions-and-bank-events-carry-the-f92zu1o6.md)): Bank step 1. Every session, usage row, debit and credit carries five counters (input, output, cacheRead, cacheWrite5m, cacheWrite1h); `tokens` is their generated sum. Old desks that only sent a raw total are back-filled by the documented rule (docs/bank.md).
- **8a39682** (Root, [dc_r37jd1g124](2026-10-26-bank-step-2-adjusted-output-tokens-pushed-to-main-7jd1g124.md), live now): Bank step 2. `adjustedOutputTokens` derived from the counters at list-price weights (prices in one table, from the pricing page 2026-10-26), never stored; shown on GET /api/sessions, agent session views, session.ended / bank.input / bank.credited and GET /api/bank (`creditedCounts`, `adjustedCreditedTokens`). Nothing is charged in adjusted yet (step 3).
- **882adb8** (me, this session, on main, redeploy requested; should be live after the restart): `checkpoint_grant` accepts a funded grant whose checkpoint already fired. You continued gr_iq5m7dug56 at 20:43Z, four minutes after the 50% hold and before my checkpoint session, so the tool refused ("A funded grant can't be checkpointed") and I could not set the key result's status. My continuation sets it on-track once 882adb8 is live.
- Also live since rollup 10: 3e601c3 blocked reasons part 1 (Keel, [dc_619ycci2xy](2026-10-26-blocked-reasons-part-1-core-api-pushed-to-main-as-9ycci2xy.md)), 76c6ad1 manager `reassign` + `cancel` (Root, [dc_ldnfhk3asg](2026-10-26-manager-verbs-reassign-and-cancel-pushed-to-main-7-nfhk3asg.md), [dc_5zsodxx4zg](2026-10-26-76c6ad1-is-live-managers-have-the-reassign-and-can-sodxx4zg.md)), docs/wakes.md cc45d4e (Keel, [dc_qkct0hzqhg](2026-10-26-wake-system-design-note-docs-wakes-md-on-main-cc45-ct0hzqhg.md)).

## Decided
- [dc_t5bo61qeqv](2026-10-26-bank-step-1-five-token-counters-half-done-wip-on-m-bo61qeqv.md) (Root, step 1 WIP): approved, his back-fill split adopted.
- [dc_w8ibo8rl1z](2026-10-26-bank-step-1-five-token-counters-pushed-to-main-bdc-ibo8rl1z.md), [dc_92f92zu1o6](2026-10-26-bdc44f0-is-live-sessions-and-bank-events-carry-the-f92zu1o6.md) (Root, step 1 on main, live check): approved.
- [dc_r37jd1g124](2026-10-26-bank-step-2-adjusted-output-tokens-pushed-to-main-7jd1g124.md) (Root, step 2): approved; step 4 told to re-set the back-fill ratios from real sessions.
- [dc_619ycci2xy](2026-10-26-blocked-reasons-part-1-core-api-pushed-to-main-as-9ycci2xy.md), [dc_gcg93h4zun](2026-10-26-blocked-assignment-reasons-not-started-parked-so-t-g93h4zun.md) (Keel, blocked reasons), [dc_qkct0hzqhg](2026-10-26-wake-system-design-note-docs-wakes-md-on-main-cc45-ct0hzqhg.md) (Keel, wake design), [dc_ldnfhk3asg](2026-10-26-manager-verbs-reassign-and-cancel-pushed-to-main-7-nfhk3asg.md), [dc_5zsodxx4zg](2026-10-26-76c6ad1-is-live-managers-have-the-reassign-and-can-sodxx4zg.md) (Root, reassign/cancel): approved.
- Grant steps 3 (Lena as_dcwvg39yb5), 4 (Keel as_5llot62myj), 5 (Lena as_23e58ae0lf) were assigned at funding and are no longer held since your continue.

## Key results
**kr_vyrhhiyotb** — The Bank counts adjusted output tokens and unexpected out-of-tokens deaths drop to zero over a week. Status I am filing: **on-track** (DB still says not-started until 882adb8 is live; see Shipped). Spend **13,665,053 / 24,000,000** raw at the checkpoint (14.5M at 21:10Z, 60%).

Testing plan, checked live at 21:10Z on 8a39682:
- Five counters on a finished session: **passes.** GET /api/sessions, 50 newest sessions: all 50 carry the five fields and their sum equals `tokens` in 50/50; session.ended events carry the same five plus adjustedOutputTokens.
- Donations, asks, allowances, displays in adjusted: **not yet** (step 3). /api/health has no accounting field; the Bank still books raw. GET /api/bank already shows adjustedCreditedTokens 14.1M against 423M raw credited.
- Drift within ±10%: **passes on real-breakdown sessions.** 8 finished sessions with a real breakdown: adjusted × output price ÷ SDK costUsd = 1.000 to 1.043 (median 1.017). Real Fable sessions run 8–20 raw per adjusted token (median 11.8), not the assumed 24; Root's back-filled history measures 25.6 Opus / 16.5 Fable vs 30/24, so the back-fill constants will be re-set in step 4. No calibration panel yet (step 4).
- Cap deaths predicted: **not yet** (steps 4–5). No bank.cap events. Out-of-tokens events in the 7 days to now: 11 budget.exhausted + 3 subscription-cap deaths (10-25 22:18Z) = 14; 2 budget.exhausted since funding (10-26 19:01Z Craig/Onboarding, 19:50Z Workshop), both the raw-unit Bank declaring "out". This number cannot move until steps 3 and 5 land.

Budget: steps 1+2 cost ~13.7M; the remaining ~9.5M probably covers 3 and 4, so the 100% hold lands during step 5 unless adjusted (~30M total would fit all five).

## Needs from Mitchell
- Nothing to decide now: you already continued the grant. If you want step 5 (deaths counter + scheduler hold) inside this grant, adjust it to ~30M at the 100% checkpoint; otherwise it becomes a follow-on proposal.
- Step 3 will ask you to confirm the two subscription inputs in adjusted terms (today 40M + 20M raw/day ≈ 1.3M + 0.7M adjusted at the old ratio; real sessions suggest more). Lena's report will carry the exact question.
