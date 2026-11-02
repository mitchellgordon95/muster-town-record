---
id: "dc_eysmkcbp45"
type: "report"
state: "building"
title: "Desk perf step 2: desk-steal alert merged (PR #95, c229d63); parked for the live test alert"
authorId: "ag_yazt68nezn"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Decision on thresholds: desk-steal KEEPS 50 %/35 %/25 % as the funded plan says. Red on nearly every long fork session is the true state of shared-CPU desks (84–91 % measured), and that alert is the evidence step 3 (move desks to performance CPUs) needs; the fix is the cause, not the threshold. Hourly re-alert stays the same as the other red metrics. Mitchell gets this as \"Your call\" in rollup #19. The continuation as_vt8eovf938 (deploy c229d63) runs the test alert as written; no re-assign."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T23:19:36.009Z"
sessionId: "se_lymp8o1o41"
assignmentId: "as_lrnuw10ad9"
costUsd: 1.340805
tokens: 67040
turns: 28
createdAt: "2026-10-29T23:19:07.518Z"
updatedAt: "2026-10-29T23:19:36.009Z"
---
## What I did
- Added a `desk-steal` metric to packages/server/src/monitor.ts (`deskStealMetric`). It reads desk sessions from the sessions table (backend != host, wallMs ≥ 5 min, cpu/steal measured) that ended since the last sample.
  - **Red:** one session with steal share (steal / (cpu + steal)) ≥ 50 %, or two sessions ≥ 35 % within an hour.
  - **Yellow:** ≥ 25 %, shown in town only.
  - **Clears:** after 5 clean sessions, counted through a new optional `Reading.clean`.
  - Raise, hourly re-alert, FYI and SMS/email go through the same path as the other red metrics.
- `POST /api/admin/monitor/test?metric=desk-steal` now accepts any metric key and tags the test event with it. Any other key gets a 400.
- Added the thresholds to deploy/README.md "Monitoring".
- Added tests to test/monitor.test.ts:
  - red on one session ≥ 50 %
  - red on two sessions ≥ 35 % within an hour, but yellow when they are more than an hour apart
  - yellow at 25 %
  - clears after 5 clean sessions, not after 5 samples
  - the DB probe skips host, short, unmeasured and still-running sessions
  - the `?metric=` route
- **Checks:** monitor tests pass (22/22) and `npm run typecheck` is green. The full local suite hit my 580 s limit with 9 tests timing out at about 5 s. The 7 files those tests are in all pass when run alone. CI passed.
- Merged PR https://github.com/mitchellgordon95/muster-town/pull/95 (merge commit c229d63) and queued a redeploy (no image rebuild). The work is parked until c229d63 is live.
- Rewrote the topic page "Monitoring and alerting" ([dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md)).

## Findings
- **Measured steal (GET /api/sessions, desk sessions ended 20:49–22:56Z on 10-29):** all 7 sessions of 5 min or longer had a steal share of 84–91 %, with wall times of 22–53 min:
  - se_8m9iwp4hbt: 86 %
  - se_hq38i8l1qr: 87 %
  - se_n6o4gb6rsu: 91 %
  - se_ndpuqsaqbe: 84 %
  - se_0rlpjpxgyn: 90 %
  - se_fsvrbi1d33: 89 %
  - se_eeg8zxrn8y: 90 %
  - Short sessions on Cleo's own desk Machine read 1–13 %.
- **The default thresholds don't fit these numbers.** As instructed, I kept the defaults rather than picking new ones. Once c229d63 is live, `desk-steal` will go red on the first long fork session and will effectively never clear while desks run on shared CPUs. When ALERT_* outbound is on, it will also re-send SMS + email at most once an hour while fork sessions keep ending red, which uses 2 of the 10 messages per hour.
- Whether to raise the thresholds or rely on step 3 (moving desks to performance CPUs) is a call for the manager or Mitchell. Step 3 is not queued.
- A sample with no newly ended desk session changes nothing, so the hourly re-alert only fires when another red session ends.
- **Next session (on c229d63 live):**
  1. Check health `commit` contains c229d63.
  2. Run `POST /api/admin/monitor/test?metric=desk-steal` with an admin token.
  3. Record eventId, fyiDocId and the sms/email results. If `monitor.outbound` is still false, record the event and FYI only and don't re-ask for the secrets (outbox dc_nwv9dy37ui).
  4. Note whether a real `desk-steal` red alert has already opened in health `monitor.alerts`.

## What I need from you
Decide whether `desk-steal` keeps the 50 %/35 %/25 % thresholds even though every measured long desk session reads 84–91 % steal, which means it will be red nearly all the time.
