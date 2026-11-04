---
id: "dc_rju0tw41ou"
type: "report"
state: "building"
title: "Checkpoint for gr_kdlogzzo5s overtaken: Mitchell adjusted it to 1,500,000 before this ran; key result statuses set on the grant, PR #336 stops stale checkpoint assignments from running"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_gzw9ibc73a","dc_h7escu847w","dc_x9g4zyba1y","dc_2p1ihh4s5a","dc_kzrm3x8h5s","dc_58bp6zln1c"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/336"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on {pr: 336}. On resume: merge if green, but do NOT call redeploy (town-wide FYI dc_uzwcg5xw3u: CI promotes green main by itself); park on {deploy: sha}."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:14:02.375Z"
sessionId: "se_tur4qc17ix"
assignmentId: "as_dznfz9jmxh"
costUsd: 3.2984158499999996
tokens: 164921
turns: 31
createdAt: "2026-11-04T19:13:18.809Z"
updatedAt: "2026-11-04T19:14:02.375Z"
---
## What I did
Live ad27e6f (health read 19:03:21Z). This checkpoint assignment was created at 18:12:39Z when gr_kdlogzzo5s crossed 100% (910,950 of 900,000), but Mitchell adjusted the grant to 1,500,000 from the checkpoint card at 18:27:57Z (event 118943, [dc_gzw9ibc73a](2026-11-04-grant-gr-kdlogzzo5s-adjusted-1-500-000-tokens-w9ibc73a.md), already approved), 35 min before this session ran. The grant is funded, has no checkpoint row in the Town Hall in-tray, and the 19 sessions charged to it still sum to 910,950. So I filed no checkpoint rollup: it would have put a second card under rollup 46 (7 min old) for a decision Mitchell already made. Instead:
- Set each key result's status and evidence on the grant with `checkpoint_grant` (it accepts a funded grant whose checkpoint fired and does not re-hold it): kr_spolcs3akx on-track, kr_rl8l0xfrkm on-track, kr_nt0q4a3pmy on-track, kr_sdtzgbyrxn claimed. The grant page shows the notes.
- Fixed the cause in core: a human's continue, adjust or cut at a checkpoint now cancels the manager's still-pending "Write the checkpoint for …" assignment (heldReason names who decided). A checkpoint session already running still files. PR #336 (draft, no migration): https://github.com/mitchellgordon95/muster-town/pull/336. packages/core: 745 tests green locally, typecheck green; one new test, two old expectations updated (no pile-up of stale checkpoint assignments; the "topped up before the checkpoint session" case starts the session before the adjust).
- Rewrote wiki dc_h7escu847w (shortened) and logged.

## Findings
Key results of gr_kdlogzzo5s, 910,950 / 1,500,000 tokens (all 19 sessions on it; this one not yet booked):

| Key result | Status | Evidence |
|---|---|---|
| kr_spolcs3akx digest card first in the in-tray | on-track | Card built: #305 = 90212da live, #317 = d156a72 grouped card merged (as_4lst9z1vf8 checks it on the deploy). No card until the retainer's first fire at 07:00 UTC 11-05. |
| kr_rl8l0xfrkm approved daily retainer on the Secretary | on-track | sc_8zoclbtrwp funded 140,000 (10,000 × 14) by Mitchell at 17:18:11Z, taker ag_7tiwyqva83 on claude-haiku-5-5, 0 runs, next 07:00Z 11-05; one-shot check sc_wpigko7f0e at 07:30Z. |
| kr_nt0q4a3pmy a 1:1 decision applied by Mitchell via Secretary | on-track | Verb live (#300 = 02c40bf), "Talk to Secretary" live (#308 = 0fb0b97). No real 1:1 decision on any grant's history yet. |
| kr_sdtzgbyrxn core and server tests | claimed | #300 and #303 merged with green CI. |

Cost of the stale checkpoint: this session ran on Fable, charged to the grant, for a checkpoint nobody waited for. The same pattern (human decides from the card within minutes, the manager's assignment runs later) is what gr_cwwtrabt2o (proposed) prices; PR #336 removes the pending-assignment half of it. Open steps on the grant are unchanged: as_4lst9z1vf8 (#317 live check), as_pun71j4w1b and as_9kyqil4wi4 running, step 3e waits on Teo's #327, step 4a at 07:30Z.

## What I need from you
Nothing needed. I resume when PR #336's CI finishes: if green, merge, redeploy and say which commit should be live.
