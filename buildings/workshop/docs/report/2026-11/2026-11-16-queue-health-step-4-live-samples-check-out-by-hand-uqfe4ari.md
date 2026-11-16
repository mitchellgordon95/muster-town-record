---
id: "dc_lguqfe4ari"
type: "report"
state: "building"
title: "Queue health step 4: live samples check out by hand; all four key results claimable"
authorId: "ag_td9097n74a"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 4 of 4 done; numbers checked by hand against the 1:1. Grant gr_pdja05z2f1 closed as done with close_grant (522,644 of 700,000 spent)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-16T23:18:48.092Z"
sessionId: "se_cwdcfuqmze"
assignmentId: "as_1h7hmrre0j"
costUsd: 1.6299251000000001
tokens: 81496
turns: 28
createdAt: "2026-11-16T23:18:06.829Z"
updatedAt: "2026-11-16T23:18:48.092Z"
---
## What I did
- Read GET /api/health at 2026-11-16 23:15Z. Live is commit 5974c42b, which contains PR #466 0a674074.
- Collected every ask a human decided in the 14-day window: 111 ask.decided/retired events, and each ask read by id.
- Checked the numbers by hand against Mitchell's 1:1 mt_uarrn0kco1, using the decision times and his transcript lines.
- Read the Secretary's latest rank run, as_9gcghlmhs7.
- Rewrote topic page [dc_271txc8zem](../../wiki/2026-11/2026-11-12-queue-health-gr-pdja05z2f1-1txc8zem.md).
- I made no code change.

## Findings
**Live `legible.queue`, 14 days:**

| Type | On card (min) | First seen to decision (min) | Lines | Questions | n |
|---|---|---|---|---|---|
| money | 1.21 | 10.26 | 0 | 0 | 5 |
| policy | 2.13 | 2.13 | 1 | 1 | 5 |
| do | 2.73 | — | — | — | 6 |
| click | — | — | — | — | 0 seen of 18 decided |
| credential | — | — | — | — | 0 seen of 4 decided |

Gates: 0.94 per funded grant (31 gates over 33 grants). Budget used 0.67. Warning off.

**Samples:**
- The sample counts match by hand. After step 1 went live (11-15 21:26Z), humans decided exactly 5 money, 5 policy and 6 do asks.
- Click is 0 because all 18 click decisions were made between 11-09 and 11-15 20:55Z, before any screen view existed. No click ask has been decided since. This is missing data, not a bug. One click ask is open now, so the row fills when Mitchell decides it.
- The precondition is met: Mitchell worked the queue on 11-15 (21:31–21:43Z) and on 11-16 (18:14–18:46Z).

**Three asks checked by hand.** I assumed each card is on screen from the previous decision to its own. Policy minutes per ask are [0.47, 6.02, 5.02, 2.13, 0.12]: the median is 2.13, the same as the live value.
- **ak_bw4qlkb8rz** (policy, ledger rule): about 2.13 min on card. One line, "what is the ledger?", which is 1 question.
- **ak_r31emiv274** (policy, split L steps): about 5.0 min. One line, "wait why are we proposing getting rid of L steps? …", which is 1 question.
- **ak_zak3hakoj1** (money, retainer): about 10.3 min. Five lines, three of them questions.
- Policy lines come to [0, 2, 1, 1, 0] and money lines to [0, 1, 0, 5, 0]. Their medians (1 and 0) match live.

**Known limit:** a line counts against whatever card is on screen, not against its topic. ak_zak3hakoj1's 5 lines were about the wiki layer and pins, not the retainer. The medians absorb this, so I would not change the code for it.

**Tuning:**
- **30-minute cap:** keep it. The longest real view was about 10 min, during active talk, so the cap never applied.
- **0.5 / 0.85 thresholds:** keep them. Live is 0.94 gates per grant and 0.67 budget used, so the warning is rightly off: work stops at a gate about once per grant. The red state has not happened live yet. Only tests cover it.

**Rank run (kr_nsghrfza2i):** as_9gcghlmhs7 (11-16 07:00Z) ends with "## Queue health, last 14 days". Its numbers match legible.queue as computed at that hour. The next run (11-17 07:00Z) will carry the money and policy samples.

**Grant:** all four steps are done. The grant has spent 522,644 of 700,000 tokens. All four key results can be claimed, so the manager can close it with close_grant.

## What I need from you
Nothing needed.
