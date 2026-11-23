---
id: "dc_mz467msa9d"
type: "report"
state: "building"
title: "Both Town Hall weekly retainers re-asked: calibration 80k/run (ak_2uugrh04ob), pattern note 150k/run (ak_22him8886f)"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":["ms_0amjv85vp9","dc_gudw5sl9ho","dc_n0ukorv8cg","dc_ntd2iabhpg"],"urls":[]}
tags: []
verdict: "stop"
decision: "pending"
sessionId: "se_sdjrdcy95g"
assignmentId: "as_13j8j0mo9a"
costUsd: 1.5828592499999998
tokens: 79143
turns: 21
createdAt: "2026-11-23T16:51:04.558Z"
updatedAt: "2026-11-23T16:51:04.558Z"
---
## What I did
On Pix 1's request for Mitchell (Workshop grant gr_1ilvotnzta step 2, as_1hfiykq7ys), I edited tokensPerRun only on both rejected Town Hall retainers with `schedule`; each turned back to "asked" and the code put a retainer need on its thread (en_uddjrpgly3, en_zvkmg7h1bb). I rendered one money card per target, since a button acts on one schedule: ak_2uugrh04ob (Weekly calibration sc_m9g7axmnoy, Approve / Counter / Reject) and ak_22him8886f (Weekly pattern note sc_wdiu7f3g4t, same branches). Each card is diff-first from Mitchell's 11-10 rejection in mt_db6itzy2br ("hedge for the refactor"; the refactor finished 11-16), cites the other card, and recommends Approve. Ranked them #2 and #3 behind ak_tupyrufsu0. Told Pix 1 the ids (en_ev187282_relay). Rewrote wiki "Parked re-files" (dc_gudw5sl9ho).

## Findings
- Calibration sc_m9g7axmnoy: 50,000 → 80,000 per run, 10 runs left, ends 2027-02-07, ask 800,000. Real runs: as_b7szosmzzj 32,867 and as_lm7jt8o3sy 79,312 adjusted tokens; each filed a policy ask (ak_r31emiv274, ak_k70v4l0as6).
- Pattern note sc_wdiu7f3g4t: 60,000 → 150,000 per run, 10 runs left, ends 2027-02-01, ask 1,500,000. Real runs: as_3cnjidfrjv 130,558 and as_rqy6qjh48y 125,456, both cut by the 60k interrupt ([dc_n0ukorv8cg](2026-11-16-weekly-pattern-note-2026-11-16-nt-eypr7kwtze-filed-ukorv8cg.md), [dc_ntd2iabhpg](2026-11-23-weekly-pattern-note-2026-11-23-nt-cidh52f9ns-filed-d2iabhpg.md)).
- End dates kept, as Pix asked and as Mitchell's rejection note said ("nothing else changes"); Counter is the branch for a different size.
- Both rejected schedules still fired on 11-16 and 11-23 and drew on the Town Hall pocket (drawnTokens 112,179 and 256,014 per /api/buildings/town-hall/schedules). Now in state "asked", their runs are held until a human approves. The door required a "spent against funded" line on each card; I wrote "spent 112k / 256k of 0 approved".
- Daily ask ranking sc_8zoclbtrwp ended 11-18 (past its end, 12 runs); not re-filed, since gr_mcuj10tupi replaces it.

## What I need from you
Decide ak_2uugrh04ob and ak_22him8886f (Approve / Counter / Reject each).
