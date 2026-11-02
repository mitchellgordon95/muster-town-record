---
id: "dc_gac5p4math"
type: "report"
state: "building"
title: "Workshop's first grant proposed (gr_jqsqra0dlx, 275M tokens): KR1–3 work queued in the grant lane and held until Mitchell funds it"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_pd9sqy2vvn","dc_16g7lkpj46","dc_jd3rl25rgr"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grant filed and grant-lane work queued per town hall decision 2; nothing more to do in the building until Mitchell decides gr_jqsqra0dlx. Escalating the funding ask in the rollup."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T16:44:08.855Z"
sessionId: "se_5dublrhefi"
assignmentId: "as_tzh0rjwbay"
costUsd: 1.7775664
tokens: 20189
turns: 22
createdAt: "2026-10-25T16:43:43.216Z"
updatedAt: "2026-10-25T16:44:08.855Z"
---
## What I did
Filed the grant agreed in the town hall ([dc_pd9sqy2vvn](../../../../../library/meeting-notes/2026-10/2026-10-25-town-hall-town-hall-notes-9sqy2vvn.md), decision 2) with `propose_grant`; it is in the Town Hall in-tray as gr_jqsqra0dlx, status proposed. Queued one assignment per key result in the grant lane (Root, Lena, Keel); all three are held with "grant not funded yet" and start by themselves when the grant is funded, so funding is the only prompt the building needs. Told Kelly one concrete finding for the wake audit (decision 3). Wiki pages "Waterfall design" and "Notes" rewritten.

## Findings
- **Proposal gr_jqsqra0dlx.** Objective: the Workshop runs itself in goal-directed mode, working whenever it can and showing why when it can't. KR1 kr_zrjhc51fc4 (work in flight without a human prompting), KR2 kr_a3qo30oe5b (exactly one blocker from the fixed set plus what unblocks it), KR3 kr_tezc1nboh6 (fund / approved checkpoint / new KR wakes the manager within one cycle). Stop condition: all three verified live by a human, or 100% spent, or cut at a checkpoint, or a KR needs a BUDGET_POLICY change only a human can make.
- **Token ask = one week of recent burn.** Workshop residents spent 224.8M tokens from the building's creation (2026-10-20 00:17 UTC) to 16:40 UTC today, 5.68 days, about 39.6M tokens/day; x7 = 277M, rounded to 275M. Sage (stopped) accounts for 42.5M of that; without Sage a week is about 225M. Grants don't reserve tokens (grantReservations false), so this is a ceiling with checkpoints at 50% (137.5M) and 100%.
- **KR3 gap confirmed in code.** In core/src/grants.ts `decide`, counter, reject and cut call notifyManager; fund, continue and adjust only fire a grant event, and adding key results wakes nobody. Managers are woken by in-tray reports and meetings only. Root's assignment closes this; Kelly's audit (decision 3) is its input.
- **Assignments, all held until funding:** Root as_gz2yaa0s7u (KR3 wake path + KR1 prompt line naming funded KRs with nothing in flight), Lena as_gyi0qt04yo (KR2: derived `blocker` in core with five states and an unblock string, shown on the building panel), Keel as_1znskqwqoh (KR1 baseline at funding time, then live checks of KR2/KR3 once their commits are on prod, parking on deploy if not). Keel's parked step-4 check of the flip (as_x90ojbaxql) still resumes ~20:00Z.
- Live: commit 4d6a941, Workshop budgetMode goal-directed, pool general, explorationTokensPerDay null (default share), pool expiring tokens ~24M, durableTokens still −708,477.

## What I need from you
Fund or counter gr_jqsqra0dlx in the Town Hall in-tray; the three queued assignments start on their own once it is funded.
