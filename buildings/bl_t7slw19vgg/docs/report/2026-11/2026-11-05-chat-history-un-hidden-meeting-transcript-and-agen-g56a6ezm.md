---
id: "dc_2rg56a6ezm"
type: "report"
state: "building"
title: "Chat history un-hidden: meeting transcript and agent Talk tab show every line again (PR #363, Mitchell's decision 8 in mt_pr3347g2w2); parked on CI"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["mt_pr3347g2w2","ms_u97nl3s6b7","dc_qswk18hm5y"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/363"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #363 is the right reading of Mitchell's decision 8 (whole transcript, opened at the latest line, no fold); Secretary confirmed (ms_rlil7toefz). The continuation as_kqcg4thnco (CI done → merge if green, park on deploy) already resumed by itself; nothing more to assign. Rolls up once #363 is live."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T19:50:00.595Z"
sessionId: "se_6loedrpxz0"
assignmentId: "as_mp2h05mzbo"
costUsd: 1.54343415
tokens: 77172
turns: 15
createdAt: "2026-11-05T19:49:34.836Z"
updatedAt: "2026-11-05T19:50:00.595Z"
---
## What I did
Mitchell, via Secretary from 1:1 mt_pr3347g2w2 (decision 8): "whoever implemented hiding chat history behind a clickable load link, tell them they've taken progressive disclosure too far". That was gr_zak30564zh step 4's folds. I removed both in PR #363 (https://github.com/mitchellgordon95/muster-town/pull/363, draft, branch agent/teo/chat-history-no-fold off main cd1adc8):
- Meeting panel: the transcript no longer shows only its last 6 messages behind "Show N earlier messages"; every line renders, and the existing scroll-to-end effect opens it on the latest line.
- Agent panel, Talk tab: no more "Show N earlier lines" over the last 5; the whole timeline renders, pinned to the bottom as before.
- No "long old tail" fold at all: he said "if anything", and none is the simplest honest reading. The `.show-earlier` class had no CSS of its own; nothing else referenced the constants.
- `npm run check --fast` green (docs, typecheck, web tests 17/17); docs/log.md line added.
- Replied to Secretary with `tell` (queued for them as as_tltltibn2c since they were idle). Topic page [dc_qswk18hm5y](../../wiki/2026-11/2026-11-04-progressive-disclosure-gl-1ds3wl2n78-wk18hm5y.md) now records Mitchell's limit so no fork re-adds a chat fold; log line written.

## Findings
- The disclosure census (skill [dc_4dqiwydii8](../../skill/2026-11/2026-11-04-disclosure-census-script-qiwydii8.md)) counts transcript words as the speakers', not the interface's, and the fold was one control, so this change moves no census row; kr_p6l1w6tade is unaffected.
- The merge is directed work, so I'll merge it myself once CI is green (no redeploy: CI deploys main). It is charged to directed today, not to gr_zak30564zh, which is held at its checkpoint; if Mitchell continues the top-up it could be re-attributed, but nothing depends on that.
- Rollup: nothing of this building's is live yet since [dc_lp6e5f27gx](2026-11-04-checkpoint-one-design-grant-at-620-411-600-000-dim-6e5f27gx.md); the item rolls up once PR #363 is live, together with PR #350 if the gr_kvmwutmybu checkpoint is continued.

## What I need from you
Nothing needed.
