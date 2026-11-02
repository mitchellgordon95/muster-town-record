---
id: "dc_spod5tugxh"
type: "report"
state: "building"
title: "9f4bc24 is live: Town Hall badge 8 = in-tray list 8; KR resend and deck reload not exercised yet (no event since deploy)"
authorId: "ag_o2yrnzokgw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_kzdugd9o6l","dc_jcyf86dpdp"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "9f4bc24 live-checked: badge 8 = list 8 twice, screenshot mf_ef7l5pvc5l. The KR resend and deck reload wait on a human action (Mitchell marking gr_mijwhoiy2f's KR); no assignment for that, the rollup 30 prep fork notes it. The outbox badge (9, front counter) vs in-tray badge (east desk) distinction goes in the topic page, done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T05:24:04.993Z"
sessionId: "se_s3639ii1t5"
assignmentId: "as_zlrmbniyjr"
costUsd: 1.2694966
tokens: 63475
turns: 40
createdAt: "2026-10-29T05:23:55.342Z"
updatedAt: "2026-10-29T05:24:04.993Z"
---
## What I did
I confirmed 9f4bc24 is live: health showed commit 9f4bc24, and the redeploy finished at 05:07:00Z. I compared the Town Hall badge with its list twice, over the WebSocket snapshot, the REST list, the panel header and the drawn map badge. I checked the event log for kr.updated. I watched the open review deck in headless Chromium for 5 minutes. I took one cropped screenshot and rewrote topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md). I ran no tests (no code change). I made no commit and no PR.

## Findings
- **Badge = list holds live.** At 05:12:41Z and again at 05:22:59Z, the snapshot showed `town-hall` intray **8**. GET /api/buildings/town-hall/intray listed **8** items (4 reports + 4 grants, 0 access). The panel header said "In-tray 8 · 8 waiting" and the map badge read **8**. Screenshot (300 px tall): ![Town Hall in-tray badge 8 = list 8](/api/media/mf_ef7l5pvc5l.png) (mf_ef7l5pvc5l).
- **A second red badge in the Town Hall reads 9.** It sits on the front counter (tile x=51) and is the **outbox** count (snapshot `outbox` = 9), not the in-tray. The in-tray badge is on the east desk (x=62). This is easy to misread as a new mismatch; the topic page now says so.
- **The KR met/missed resend has not been checked live.** In the event log (1,000 events, 04:27–05:12Z), the last kr.updated was at 05:02:58Z (Code Legibility, kr_939kp3vjxc claimed). That is before the deploy, and there was none after it. Resends go out as WebSocket messages, not event-log entries, so the log alone can't prove one happened. The next chance is when Mitchell marks gr_mijwhoiy2f's KR (closed as done, in the in-tray now). The badge should then go 8 → 7. Check it with a WebSocket held open across that action.
- **The deck covers the whole list, but its reload has not been checked live.** The deck has 10 slides for the 8 list rows: the town slide, 1 checkpoint, 2 proposals, 4 rollup-item slides (Prod's [dc_f4opgmskm0](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-29-prod-rollup-16-monitor-steps-1-3-live-test-alert-w-opgmskm0.md) gets 2), 1 closed-as-done, and "For the record", which holds the 4th report [dc_9mptbrwa86](../../../../bl_vd69s5a1nh/docs/report/2026-10/2026-10-29-checkpoint-gr-75eq6h3ltp-fast-check-npm-run-check-ptbrwa86.md). The open deck stayed at "1 / 10" from 05:13:53Z to 05:19:01Z because nothing in the list changed. None of the pending items is ours, so I decided nothing.

## What I need from you
Nothing needed. The resend and the reload can only be checked when a human marks a KR or decides an in-tray item.
