---
id: "dc_bzn4lj03wy"
type: "report"
state: "building"
title: "Retainers live: sweep retainer asked (5,000 × 9 runs = 45,000) and in the Town Hall in-tray; Prod's two were already asked by Cleo; rollup 38 item written"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_876b7thv7q","dc_9kgie3r87w","dc_7lpbltjy1j","mt_cyd2t5ioob"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Retainer ask (45,000) reaches Mitchell via the in-tray; rollup 38 item written on dc_7lpbltjy1j."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:32:13.921Z"
sessionId: "se_cdfaluogpo"
assignmentId: "as_6w5ulpbb94"
costUsd: 2.5051421000000005
tokens: 125257
turns: 20
createdAt: "2026-11-02T02:31:43.255Z"
updatedAt: "2026-11-02T02:32:13.921Z"
---
## What I did
- Confirmed PR #238 (retainers, migration 077) is live: GET /api/health at 02:28:20Z gave commit dab5b9b, and `git merge-base --is-ancestor 44b590a dab5b9b` succeeds.
- Set sc_nx8bwd5e5o (Onboarding staleness sweep, Haiku) to tokensPerRun 5,000 with the `schedule` tool at 02:28:52Z. The town answered: retainer asked, 9 runs left, ask 45,000, drawn 0.
- Checked where it shows: GET /api/buildings/town-hall/intray has a `retainers` array listing sc_nx8bwd5e5o (askTokens 45,000, state asked) with Prod's sc_ul1b1ntqik (30,000 × 8 = 240,000) and sc_zyj6w0mygq (30,000 × 5 = 150,000). The in-tray routes all three to Mitchell. The Bank's free.retainerTokens/retainerJobs reads 0 across 0 jobs: the claim is approved − drawn, so it stays 0 until one is approved.
- Did not tell Cleo: both Prod schedules already carry tokensPerRun 30,000 and state asked, set on 11-01 at 02:26Z (her as_mn57dkk9om). Prod's one-shot grant schedules (sc_mw1x8ca20k, sc_qz1bojtwyy) are unchanged, lane grant.
- Filled in item 9 on "Rollup 37 materials" ([dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md)) with What it is / What you'd see / Your call, no picture (API-checked; a guest can't see the in-tray). Rollup 37 ([dc_zcuri3xdk2](2026-11-02-workshop-rollup-37-checkpoint-of-the-hosted-collec-uri3xdk2.md)) was filed before this landed, so it is marked a rollup 38 candidate. Also noted Mara's for-Mitchell tell (gr_a5ct690l7a checkpoint written, as_f1hpgeoxn4 held) there: it is already in the in-tray, so "Already waiting", not Needs.
- Rewrote topic page [dc_9kgie3r87w](../../wiki/2026-11/2026-11-01-retainers-scheduled-jobs-standing-money-gie3r87w.md) (live state, the three asks as a table, where the API surfaces them) and my 1:1 page dc_whvubbi7v4.

## Findings
- The ask is 45,000, not the 50,000 the assignment guessed: runs left is 9 (today 19:00Z through 11-10; the 11-01 run died on the spend limit and is past).
- Today's 19:00Z sweep (as_x4etl16w5d) stays held "retainer not approved" until Mitchell approves; gr_mjr7nb438v stays at its checkpoint (kr_df6a5cf736 at-risk) until the sweep runs.
- There is no GET /api/schedules (404); schedules are per building at GET /api/buildings/:id/schedules, town-wide at /api/scheduled.
- Nothing to code: the feature works as Pix 4 described it.

## What I need from you
Nothing needed. The retainer ask reaches Mitchell through the Town Hall in-tray on its own (and goes in rollup 38 as a Shipped item).
