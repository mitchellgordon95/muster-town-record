---
id: "dc_w1l2a32d2c"
type: "report"
state: "building"
title: "Retainers: both Prod schedules sized at 30,000 tokens/run (asks 240k + 150k); parked on deploy 44b590a to file them once the tool has tokensPerRun"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["ms_z4gte88txs","dc_voni3twwz2","dc_u1zxop6ici","dc_2ns1jgf0fu"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: the continuation (parked on deploy 44b590a) files both retainer asks (sc_ul1b1ntqik 8 × 30,000 = 240k; sc_zyj6w0mygq 5 × 30,000 = 150k), checks whether sc_534iipcmzz was converted too, and tells Pix for Mitchell. No separate assignment needed."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T02:24:00.503Z"
sessionId: "se_fzgkw2907b"
assignmentId: "as_mn57dkk9om"
costUsd: 1.4931502500000002
tokens: 74658
turns: 17
createdAt: "2026-11-01T02:23:25.535Z"
updatedAt: "2026-11-01T02:24:00.503Z"
---
## What I did
- Read Mitchell's message (via Pix 1, 1:1 mt_cyd2t5ioob decision 2) and the retainer rules on main (docs/how-work-gets-done.md §7a, docs/bank.md "Retainers").
- Sized the two affected schedules from past check-style runs in my log, replied to Pix for Mitchell (Pix 1 had retired; the tell reached Pix), approved the parked step-2 report [dc_w0mppbg8tr](2026-11-01-gr-6qlj35wnh3-step-2-pr-246-merged-as-244d9d1-park-mppbg8tr.md) (PR #246 merged as 244d9d1; its live check as_f09fkpl4xt waits on the deploy), and rewrote my Notes page.
- A redeploy was waiting on this session, so I did not wait for it.

## Findings
- The `schedule` tool in this session has no `tokensPerRun` field: migration 077 and the new parameter arrive with the redeploy (44b590a is on main at 244d9d1). The asks can only be filed once that build is live, so this work parks on deploy 44b590a.
- Sizing evidence (adj. tokens per comparable one-shot check): morning check 10-30 41,436 ([dc_voni3twwz2](../2026-10/2026-10-30-morning-check-10-30-05-05z-nightly-backup-landed-0-ni3twwz2.md)), morning check 10-31 13,049 ([dc_u1zxop6ici](../2026-10/2026-10-31-morning-check-2026-10-31-backup-landed-04-17z-moni-zxop6ici.md)), 02:00Z lag sample 30,392 ([dc_2ns1jgf0fu](2026-11-01-kr-1a69c0a3be-02-00z-backup-run-held-lagms-at-109-s1jgf0fu.md)). Chosen: 30,000 per run for both, because a run that reaches tokensPerRun is asked to wrap up and a clean check costs about half that.

| schedule | job | runs left | per run | ask |
|---|---|---|---|---|
| sc_ul1b1ntqik | gr_w9ue1k1p0c step 3: daily check redeploys no longer orphan sessions (05:20 UTC) | 8 | 30,000 | 240,000 |
| sc_zyj6w0mygq | gr_ba0juhlm7n step 3: a day of hourly backups checked (05:35 UTC) | 5 | 30,000 | 150,000 |

- On resume: file both with `schedule`, check whether the morning check sc_534iipcmzz was also converted (it is repeating), and tell Pix for Mitchell. The asks then appear in the Town Hall in-tray under "Retainers for scheduled jobs" for Approve/Counter/Reject.
- Commit that should be live after the waiting redeploy: 244d9d1 (includes 44b590a).

## What I need from you
Nothing needed.
