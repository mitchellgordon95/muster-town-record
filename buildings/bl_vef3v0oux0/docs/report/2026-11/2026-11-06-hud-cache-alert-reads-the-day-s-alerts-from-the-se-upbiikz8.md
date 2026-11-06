---
id: "dc_3rupbiikz8"
type: "report"
state: "building"
title: "HUD cache alert reads the day's alerts from the server and skips the old share-format false alarms: PR #386 in CI, parked"
authorId: "ag_qsdg7umosv"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #386 (HUD cache alert from server, skips old share-format alarms) in CI, parked on {pr: 386}; continuation resumes itself. PR #364 already live as 5dc50c70. Closing gr_lwgus14rd2 waits for both #362 and #386 to be verified live."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-06T04:42:45.940Z"
sessionId: "se_6iebyc3pos"
assignmentId: "as_ail5blil47"
costUsd: 1.0860905000000003
tokens: 54305
turns: 12
createdAt: "2026-11-06T04:42:33.593Z"
updatedAt: "2026-11-06T04:42:45.940Z"
---
## What I did
- **PR #364:** it was already squash-merged as 5dc50c70 and has been live since 04:19:57Z (/api/health). Nothing left to do there.
- **HUD fix:** opened PR #386 (https://github.com/mitchellgordon95/muster-town/pull/386) for the HUD flaw found in [dc_lgh99v9tvd](2026-11-05-cache-miss-alert-pr-326-verified-live-in-the-event-h99v9tvd.md). It is in CI and I parked on it.
- **Plan page:** rewrote [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md).

## Findings
**What PR #386 changes:**
- GET /api/events accepts two new filters, `alert=` and `from=` (backed by core `EventQuery.alert`).
- The web loads the last 24 h of `alert: cache-miss` events into store `cacheAlerts`, at boot and on every reconnect. The HUD's "Cache alert" line now stays up even after the alert drops out of the client's latest 300 events.
- **Old false alarms are skipped (Nell's live finding):** `cacheMissAlert` counts only alerts with a numeric `payload.busting`. Today's two old cache-write-share alerts (ids 135616 and 135623, payload `reasons`, no `busting`) would otherwise have put the line back for every viewer until 00:00Z. This skip is the answer to Mitchell's "can we turn off the alert?": the false alarm is off, and the real prefix-busting alert stays on.

**Timing flaw:** already handled in 5dc50c70. A purpose is only judged after `MIN_SESSIONS` = 5 ended sessions with a signal, and it is re-checked across the day, not on the first session at midnight.

**Tests:**
- Added: a web test that an alert read from the server shows and that an old-format alert never shows, and a server test for `/api/events?alert=&from=`. Typecheck passes and the new tests pass.
- Full `npm run check` on my desk did not pass. On the first run one test failed: a timing assertion (`maxGap < 100` ms) that has nothing to do with this change. A second run also stopped at the tests stage, but its output named no failing test. CI on #386 is the real check.

**Next session:** squash-merge #386 when it is green, park on its deploy, then check live that GET /api/events?alert=cache-miss returns only the two old ones and the signed-out HUD shows no "Cache alert". kr_f49co6lg51 can be claimed after that. The grant closes once #362 (kr_avafh64h02) is verified live too.

## What I need from you
Nothing needed.
