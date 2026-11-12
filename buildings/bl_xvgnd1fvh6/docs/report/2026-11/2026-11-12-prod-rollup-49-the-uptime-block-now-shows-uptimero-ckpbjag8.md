---
id: "dc_idckpbjag8"
type: "report"
state: "building"
title: "Prod rollup #49: the Uptime block now shows UptimeRobot's number with no agent in the loop; seven desk deaths today diagnosed and fixed in #440"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_hcmusmivk2","dc_qldp5dch15","dc_0a4ifk957k","dc_pxthd1d0wt","dc_x3fbzp82dz","dc_olqgsgl8oq","dc_vnyqdy2c7f","dc_2flyb8z736","dc_gosea45h48"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/437","https://github.com/mitchellgordon95/muster-town/pull/438","https://github.com/mitchellgordon95/muster-town/pull/440","https://github.com/mitchellgordon95/muster-town/pull/441"]}
tags: ["rollup","untyped-asks"]
verdict: "continue"
decision: "pending"
sessionId: "se_xo78tdrukd"
createdAt: "2026-11-12T18:52:24.054Z"
updatedAt: "2026-11-12T18:52:24.054Z"
---
Live: 6185b99 since 2026-11-12 18:45 UTC (carries #437 and #438, the UptimeRobot read). #440 (desk fixes) merged as 210b4262 at 18:51 UTC and is on its way to live by CI; #441 (status link) waits on CI.

## Shipped

**1. The Uptime block reads UptimeRobot directly: no pinger agent, no prober role**
**What it is:** You asked this morning why uptime should be mediated by an agent. It no longer is. The server reads your UptimeRobot monitor behind a 5-minute cache and shows its 30-day number; the probe endpoint, the prober role and the Pinger's posting are gone (migration 113 deletes the role row, additive). The live number is 100 % and matches UptimeRobot's own API and the status page to the decimal. Reports [dc_hcmusmivk2](2026-11-12-probe-path-removal-pr-437-open-waiting-on-ci-musmivk2.md), [dc_0a4ifk957k](2026-11-12-step-1-merged-437-step-2-pr-438-open-waiting-on-ci-4ifk957k.md), [dc_pxthd1d0wt](2026-11-12-437-live-probe-post-404-438-merged-as-6185b997-wai-thd1d0wt.md), [dc_x3fbzp82dz](2026-11-12-api-uptime-live-from-uptimerobot-100-matches-statu-fbzp82dz.md) under gr_hbz0twkfp9.
**What you'd see:** muster.town signed out (Skip the tour) and Bank › Hosting › Uptime: "100% up over the last 30 days · Measured by UptimeRobot; it watched 1.7% of the window", 29 grey days and today green, 115 restarts in the window. One gap: "Measured by UptimeRobot" is not yet a link, because you saved the status-page secret as UPTIME_STATUS_URL and the code read UPTIMEROBOT_STATUS_URL. PR #441 accepts either name and merges on green CI; nothing for you to re-paste. No new screenshot was uploaded this time; the picture in rollup #47 shows the same block before it had a number.
**Your call:** None.

**2. Seven desk sessions died today with "desk exited -1"; both causes found and fixed in PR #440**
**What it is:** You asked about the Workshop's desk deaths via Pix. Cause 1: PR #434 (16:40 UTC) turned off vitest isolation; a full core test run on a 2 GB desk eats 1.2 GB in 67 s, the guest freezes and the session dies mid-work (five deaths). Cause 2: when the runtime gave up on a frozen desk it re-queued the work onto the same frozen Machine, which died again with 0 tokens (three deaths, one Machine took three sessions). Not the 6 h Machine lifetime: every stop was the runtime's own. Reports [dc_2flyb8z736](2026-11-12-desk-exited-1-two-causes-found-vitest-isolate-fals-lyb8z736.md), [dc_gosea45h48](2026-11-12-440-merged-as-210b4262-desk-1-fixes-parked-until-i-sea45h48.md), [dc_olqgsgl8oq](2026-11-12-session-ended-without-a-report-why-did-three-desk-qgsgl8oq.md), [dc_vnyqdy2c7f](2026-11-12-message-from-mitchell-via-pix-fourth-desk-death-in-yqdy2c7f.md).
**What you'd see:** After 210b4262 is live, no more -1 deaths from a test run; the Planning desk's System tab shows the deploy. API-only change: no picture.
**Your call:** PR #440 edits the vitest configs Code Legibility's #434 introduced: desks keep isolation, CI keeps the speed-up. Mara was told. Say so if you would rather Mara own that change.

## Decided
- [dc_hcmusmivk2](2026-11-12-probe-path-removal-pr-437-open-waiting-on-ci-musmivk2.md) → approve (step 1, PR #437 open: probe path and prober role removed)
- [dc_qldp5dch15](2026-11-12-answer-to-cleo-s-request-uptimerobot-free-plan-one-dp5dch15.md) → approve (Mitchell answered the UptimeRobot clicks request "done")
- [dc_0a4ifk957k](2026-11-12-step-1-merged-437-step-2-pr-438-open-waiting-on-ci-4ifk957k.md) → approve (#437 merged as 2f0cbf73; step 2 PR #438 open)
- [dc_pxthd1d0wt](2026-11-12-437-live-probe-post-404-438-merged-as-6185b997-wai-thd1d0wt.md) → approve (#437 live, probe POST 404; #438 merged as 6185b997)
- [dc_x3fbzp82dz](2026-11-12-api-uptime-live-from-uptimerobot-100-matches-statu-fbzp82dz.md) → approve (/api/uptime live from UptimeRobot, 100 % matches; PR #441 for the status link)
- [dc_olqgsgl8oq](2026-11-12-session-ended-without-a-report-why-did-three-desk-qgsgl8oq.md) → redirect (first desk-death investigator died the same way; re-assigned with the Machine-events lead)
- [dc_vnyqdy2c7f](2026-11-12-message-from-mitchell-via-pix-fourth-desk-death-in-yqdy2c7f.md) → approve (Pix relayed the fourth Workshop death; passed to the live investigation)
- [dc_2flyb8z736](2026-11-12-desk-exited-1-two-causes-found-vitest-isolate-fals-lyb8z736.md) → approve (two causes with Fly Machine events and a memory measurement; PR #440)
- [dc_gosea45h48](2026-11-12-440-merged-as-210b4262-desk-1-fixes-parked-until-i-sea45h48.md) → approve (#440 merged as 210b4262, parked until live)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_hbz0twkfp9 Uptime block reads UptimeRobot's free plan | kr_z7fw2zsmu6 probe path and prober role gone | claimed on live: POST /api/uptime/probes answers 404 | about 141,000 booked plus the live-check session / 250,000 |
| gr_hbz0twkfp9 | kr_xu6x845ycp block shows UptimeRobot's % with a status-page link | % live and matching; the link waits on #441 | |
| gr_hbz0twkfp9 | kr_1018on6syt live check after a real deploy | queued as step 3, runs after the next deploy | |
| gr_ba0juhlm7n Cut worst-case data loss to one hour | hourly encrypted off-site copies, each restorable | step 3 held: retainer not approved; the Drill row waits on [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) | about 268,000 / 600,000 |

Spend today by lane: exploration 154,601; directed 88,548 (the desk-death investigation and the UptimeRobot plan).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 4 rollups ([dc_tzb1f3dbao](2026-11-06-prod-rollup-41-close-report-for-gr-db6ofyd0yf-bank-b1f3dbao.md), [dc_cges6f5hvy](2026-11-09-prod-rollup-43-close-report-for-gr-w9ue1k1p0c-rede-es6f5hvy.md), [dc_d82jxhl3pp](2026-11-10-prod-rollup-45-gr-8cdix9mpye-420-000-1-500-000-the-2jxhl3pp.md), [dc_zipj6mbjhe](2026-11-10-prod-rollup-46-gr-8cdix9mpye-closed-done-524-619-1-pj6mbjhe.md))._
