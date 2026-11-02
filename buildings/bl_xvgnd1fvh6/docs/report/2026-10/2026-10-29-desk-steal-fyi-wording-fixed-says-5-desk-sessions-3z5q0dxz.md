---
id: "dc_943z5q0dxz"
type: "report"
state: "building"
title: "Desk-steal FYI wording fixed: says \"5 desk sessions\", merged 69228cb, redeploy queued"
authorId: "ag_4tli3jcs33"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Text-only change, tests cover both wordings, merged 69228cb and redeploy queued. Live check folds into the next desk-steal event or the morning check; nothing further."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T23:58:12.836Z"
sessionId: "se_pl30shg31l"
assignmentId: "as_x5ifs934vy"
costUsd: 0.5722758000000001
tokens: 28614
turns: 19
createdAt: "2026-10-29T23:58:03.209Z"
updatedAt: "2026-10-29T23:58:12.836Z"
---
## What I did
I fixed the clear-condition text in the monitor's FYIs. PR https://github.com/mitchellgordon95/muster-town/pull/104 passed CI and is merged at **69228cb**. I called redeploy, so **69228cb should be live** once it finishes. I did not check it live in this session.

## Findings
- `Metric` in packages/server/src/monitor.ts now has an optional `cleanUnit`. It defaults to "samples"; `deskStealMetric` sets it to "desk sessions".
- When a desk-steal alert is raised, the FYI now says "The monitor clears this after 5 desk sessions in a row under yellow". When it clears, it says "after 5 desk sessions under yellow".
- Sampled metrics (rss etc.) still use the "samples" wording.
- Only the text changed. Clearing still works the same way, and the thresholds stay at 50/35/25.
- Tests: monitor.test.ts has 22 tests and all pass when run in the foreground. I added assertions on the FYI text for both desk-steal (raise and clear) and RSS. `tsc --noEmit` in packages/server is clean.
- I updated the topic page "Monitor internals" ([dc_orhwzyxs59](../../wiki/2026-10/2026-10-29-monitor-internals-hwzyxs59.md)).
- The old FYI [dc_qrhf8jup1j](../../fyi/2026-10/2026-10-29-cleared-red-desk-steal-desk-session-steal-5-of-cpu-hf8jup1j.md) still has the old wording. Only new raise and clear updates use the new text.

## What I need from you
Nothing needed.
