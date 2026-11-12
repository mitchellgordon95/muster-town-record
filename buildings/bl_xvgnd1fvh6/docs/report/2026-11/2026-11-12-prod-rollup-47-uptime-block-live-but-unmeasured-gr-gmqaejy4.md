---
id: "dc_92gmqaejy4"
type: "report"
state: "building"
title: "Prod rollup #47: Uptime block live but unmeasured, gr_rcj8nkbkbt cut, successor proposal gr_hbz0twkfp9 (UptimeRobot free plan) filed; deploy card change list verified"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_lu24l7s1dt","dc_1n0z3ykq8r","dc_bskxxba2my","dc_3xcwuz1kn3","dc_ow4k1e1z1q","dc_boc7bkbhzw","dc_t5ru1yhb9a"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-12T14:44:28.089Z"
sessionId: "se_5i08d3y8nq"
createdAt: "2026-11-12T14:44:28.062Z"
updatedAt: "2026-11-12T14:44:28.089Z"
---
Live: 7329790 since 2026-11-11 19:12 UTC (carries #418 uptime API, #424 Uptime block, #419, #420 deploy card).

## Shipped

**1. The Uptime block is live, and its measuring moves to UptimeRobot**
**What it is:** A stranger sees an Uptime block on the signed-out landing and at the Bank server rack › Hosting: a 30-day day strip, the outage list and the restart count, fed by the public GET /api/uptime (no sign-in). Today it reads "Not measured yet" because no outside probe ever landed: you cut the pinger-agent plan this morning and chose UptimeRobot's free plan. Cleo 1 priced that plan; it is now proposal gr_hbz0twkfp9 (three steps: remove the probe path, read UptimeRobot's monitor behind a 5-minute cache, live check), and your clicks are the outbox request [dc_8319wrnjx2](../../../../../town-hall/outbox/2026-11/2026-11-12-uptimerobot-free-plan-one-monitor-on-muster-town-a-19wrnjx2.md). Reports: [dc_lu24l7s1dt](2026-11-10-gr-rcj8nkbkbt-live-check-api-uptime-the-landing-an-24l7s1dt.md), [dc_t5ru1yhb9a](2026-11-12-uptimerobot-plan-for-a-fresh-uptime-grant-mitchell-ru1yhb9a.md), [dc_boc7bkbhzw](2026-11-12-grant-gr-rcj8nkbkbt-cut-c7bkbhzw.md).
**What you'd see:** muster.town signed out (Skip the tour) and Bank › Hosting: "Not measured yet · 0% of minutes measured", a grey 30-day strip, "104 restarts in the window, 2 unclean" (as of 11-10 22:02 UTC).
![Signed-out landing Uptime block](/api/media/mf_qtwkl1jgml.png)
**Your call:** None here: the UptimeRobot proposal and the clicks request are in your in-tray and outbox.

**2. The deploy card lists what each deploy shipped, with commit links**
**What it is:** The HUD card a signed-in viewer sees for 10 minutes after a deploy now lists each deployed commit's subject as a link to GitHub, not just a count. Cleo 1 checked it on the first real deploy after PR #420: the d30c6f8 deploy card listed both commits (d30c6f8, aaa749f) and both links resolve (a 301 from the old repo name, then 200). Report [dc_1n0z3ykq8r](2026-11-10-deploy-card-change-list-confirmed-on-the-d30c6f8-d-0z3ykq8r.md).
**What you'd see:** After the next deploy, signed in, the "Redeploy finished: N changes live" card with linked subjects; "Log →" opens the Planning desk's System tab. API-only check this time: no screenshot, the card had expired.
**Your call:** None.

## Decided
- [dc_lu24l7s1dt](2026-11-10-gr-rcj8nkbkbt-live-check-api-uptime-the-landing-an-24l7s1dt.md) → approve (live check: /api/uptime, landing and Bank block agree; kr_ay5wb5wfhd claimed on the display path)
- [dc_1n0z3ykq8r](2026-11-10-deploy-card-change-list-confirmed-on-the-d30c6f8-d-0z3ykq8r.md) → approve (deploy card change list confirmed on d30c6f8; repoUrl rename cleanup not worth a session)
- [dc_bskxxba2my](2026-11-12-message-from-mitchell-via-secretary-from-mitchell-kxxba2my.md) → approve (relay: GitHub Actions plan; superseded minutes later)
- [dc_3xcwuz1kn3](2026-11-12-message-from-mitchell-via-secretary-supersedes-my-cwuz1kn3.md) → approve (relay: UptimeRobot free plan, no pinger agent or prober role; Cleo 1 redirected)
- [dc_ow4k1e1z1q](2026-11-12-session-ended-without-a-report-gr-rcj8nkbkbt-repla-4k1e1z1q.md) → redirect (session ended without a report; Actions draft dropped; the UptimeRobot plan assigned as directed work)
- [dc_boc7bkbhzw](2026-11-12-grant-gr-rcj8nkbkbt-cut-c7bkbhzw.md) → approve (gr_rcj8nkbkbt cut by Mitchell 14:38 UTC, 288,098 of 260,000)
- [dc_t5ru1yhb9a](2026-11-12-uptimerobot-plan-for-a-fresh-uptime-grant-mitchell-ru1yhb9a.md) → approve (the plan became proposal gr_hbz0twkfp9 and outbox request [dc_8319wrnjx2](../../../../../town-hall/outbox/2026-11/2026-11-12-uptimerobot-free-plan-one-monitor-on-muster-town-a-19wrnjx2.md))

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_ba0juhlm7n Cut worst-case data loss to one hour | hourly encrypted off-site copies, each restorable | step 3 (a day of hourly backups checked) held: retainer not approved; the Drill row waits on [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) | about 268,000 / 600,000 |
| gr_rcj8nkbkbt (cut today) | kr_ay5wb5wfhd Uptime block at the rack and the landing | claimed (display path live; the number waits on UptimeRobot) | 288,098 / 260,000 |
| gr_rcj8nkbkbt (cut today) | kr_6ofa7wf812, kr_nrh9ygog2w | unclaimed; carried into gr_hbz0twkfp9 as kr_xu6x845ycp, kr_z7fw2zsmu6, kr_1018on6syt | |

Spend today by lane: exploration 0; directed 74,676 (the UptimeRobot plan and the dropped Actions session).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_rdc7hrw4q8, gr_hbz0twkfp9), 2 requests ([dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md), [dc_8319wrnjx2](../../../../../town-hall/outbox/2026-11/2026-11-12-uptimerobot-free-plan-one-monitor-on-muster-town-a-19wrnjx2.md)), 4 rollups ([dc_tzb1f3dbao](2026-11-06-prod-rollup-41-close-report-for-gr-db6ofyd0yf-bank-b1f3dbao.md), [dc_cges6f5hvy](2026-11-09-prod-rollup-43-close-report-for-gr-w9ue1k1p0c-rede-es6f5hvy.md), [dc_d82jxhl3pp](2026-11-10-prod-rollup-45-gr-8cdix9mpye-420-000-1-500-000-the-2jxhl3pp.md), [dc_zipj6mbjhe](2026-11-10-prod-rollup-46-gr-8cdix9mpye-closed-done-524-619-1-pj6mbjhe.md))._
