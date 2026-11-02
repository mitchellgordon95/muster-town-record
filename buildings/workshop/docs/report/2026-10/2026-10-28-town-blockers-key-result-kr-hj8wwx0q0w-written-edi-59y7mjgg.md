---
id: "dc_l459y7mjgg"
type: "report"
state: "building"
title: "Town blockers key result kr_hj8wwx0q0w written; edition 1 of the page (dc_nhd0maw3f5) from 41,824 events: redeploy drains cost 1,163 min and 21 killed sessions in 7 days, Mitchell's decisions wait p90 10 to 14 h"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_xjjl97wyf4","dc_nhd0maw3f5"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: KR kr_hj8wwx0q0w and Town blockers edition 1 (dc_nhd0maw3f5) done; goes under Key results in rollup 29."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T19:34:27.351Z"
sessionId: "se_7rs6bwgjmw"
assignmentId: "as_ieewvmm7fj"
costUsd: 3.3844451
tokens: 67689
turns: 26
createdAt: "2026-10-28T19:34:05.559Z"
updatedAt: "2026-10-28T19:34:27.351Z"
---
## What I did
- Wrote the key result kr_hj8wwx0q0w under the Trust objective ob_s7jsvvoe5p (source: the 1:1 notes [dc_xjjl97wyf4](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-pix-notes-jl97wyf4.md)). Rollup 29 lists it for Mitchell to keep or cut.
- Pulled the whole event log (41,824 events) and measured the last 7 days with a new script, `scripts/town-blockers.py`, committed to main at a89e410 with a docs/log.md line. No redeploy queued: it is a script, not served code, and a drain would cost the very minutes this page counts.
- Published the Workshop topic page "Town blockers" [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md), edition 1, four blockers with numbers and one proposed fix each. Recorded the standing duty (rerun the script, rewrite the page, link it) in my wiki so every rollup from 29 on carries it.

## Findings
Seven days to 2026-10-28 19:32Z, every number from the event log:
- **Redeploy drain is the biggest wait.** 97 redeploys (13.9 per day, 49 asked by CI). 86 waited for running sessions: median 9.5 min, max 56.7 min; 1,163 of the 1,177 redeploy-minutes were drain. 18 drains timed out and killed 21 sessions, whose assignments were rerun from scratch. Fix on the queue already: no-drain layer A (as_us3zlu1idf, then as_5gi7tmqp51).
- **Mitchell's decisions.** 19 proposals: median 1.2 h, p90 13.8 h, 98 h summed. 79 rollups and reports: median 0.9 h, p90 10.4 h, max 38.5 h. They come in 26 sittings for 109 decisions; the longest gap between sittings was 38.5 h. Fix proposed: the review deck (as_rj8d98dauk), oldest first with ages shown.
- **Assignments parked on a deploy.** 149 started after a median 20 min, p90 142 min, max 22.5 h. Fix proposed: a parked assignment requests the redeploy itself when none is running.
- **Budgets exhausted 11 times** (Prod 3, Workshop 2, six agents once). Fix proposed: run-out time per building on the finance page.
- Not measurable from the log: the restart gap itself (two events 2 s apart) and the rerun cost of the killed sessions (needs the sessions table). Next edition adds them.

## What I need from you
Nothing needed.
