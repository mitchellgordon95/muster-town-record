---
id: "dc_yqq9ycu5g5"
type: "report"
state: "building"
title: "53482f8 is live, but I can't run the standup + redeploy check (no meeting.facilitate, no town.redeploy); tests pass on 9b20fad"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "53482f8 verified live via tests and the event log; the live 1:1-during-redeploy check needs Mitchell and goes into rollup 6. The mt_h9xvyaiwdu self-closing standup is a separate assignment."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T04:31:11.201Z"
sessionId: "se_q0e3ia52gl"
assignmentId: "as_h9k2gr0k3c"
costUsd: 0.9190933999999998
tokens: 34869
turns: 24
createdAt: "2026-10-26T04:29:52.180Z"
updatedAt: "2026-10-26T04:31:11.201Z"
---
## What I did
- Checked that 53482f8 is live. GET /api/health shows commit 9b20fad, and `git merge-base --is-ancestor 53482f8 9b20fad` succeeds.
- Tried to call a standup to test it live. `POST /api/meetings` returned `forbidden: meeting.facilitate`. I also don't have `town.redeploy`, so I can't run either half of the planned check.
- Searched the live meetings and event log for redeploy notices instead, and ran the feature's tests on the live commit.

## Findings
- **No live meeting has a Town notice line yet.** None of the last 20 meetings has a `speakerKind: system` line. That's expected: the only redeploy since 53482f8 drained from 00:05:04Z to 00:33:09Z (28 min, waiting on Pix's work session, under the 30-min cap) and restarted at 00:33:13Z. Nothing was `discussing` at the time, so there was nothing to post a notice into. The follow-up CI redeploy at 00:33:41Z (9b20fad) also ran with no meeting open.
- **Tests on live main (9b20fad) pass:**
  - packages/runtime one-on-one, stale-state, redeploy and redeploy-lock: 39/39. These cover the 1:1 case (the manager keeps answering, the restart posts the notice, and a new session answers the lines it missed) and the standup case (a facilitation that keeps going holds the drain only drainMeetingMs, then gets the notice and stays open).
  - packages/core one-on-one: 3/3.
- **Expected live behaviour for a standup with no human in it:** the drain tells the facilitator to wrap up (drainNudgeFacilitator). Usually the standup closes within 2 min and gets no notice. The notice only shows when a meeting is still `discussing` at restart, which in practice means a human is talking. So the real live test is a 1:1 or a standup with a human in it, not one an agent facilitates alone.
- **Something unrelated:** Mitchell's standup mt_h9xvyaiwdu (00:57:11Z) went from `collecting` to `done` 3.4 s after it was created, with no summaries or lines (notes [dc_kv7sxrtacd](../../meeting-notes/2026-10/2026-10-26-town-workshop-standup-notes-7sxrtacd.md)). `ops.endMeeting` always passes `actor = null`, so the event log can't say who ended it. If Mitchell didn't click End, it's a bug worth a look.

No code changes, so there is no commit or PR.

## What I need from you
Mitchell: open a 1:1 with Pix, trigger a redeploy (or push to main) while it's open, and keep talking. The transcript should then get a "Town" line saying "Pix's reply is waiting on a redeploy (commit …)", and Pix should answer your missed lines after the restart.
