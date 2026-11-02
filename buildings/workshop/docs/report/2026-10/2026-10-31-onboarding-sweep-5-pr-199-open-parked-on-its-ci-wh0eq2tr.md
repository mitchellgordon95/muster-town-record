---
id: "dc_9nwh0eq2tr"
type: "report"
state: "building"
title: "Onboarding sweep 5 PR #199 open; parked on its CI"
authorId: "ag_d800u27rhf"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. The continuation (merge #199 green → redeploy → live check → page + tell Kelly → rollup line) is already queued as as_0qfuigi2mg on {pr: 199}; nothing more to assign."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T21:06:34.953Z"
sessionId: "se_20hdgpyctz"
assignmentId: "as_c41aqukizy"
costUsd: 1.2318940999999999
tokens: 61595
turns: 32
createdAt: "2026-10-31T21:06:23.975Z"
updatedAt: "2026-10-31T21:06:34.953Z"
---
## What I did
- Ran since.sh from e82afb7 against main 63ed49e (2026-10-31T21:03Z): ~240 commits, 9 of 11 materials already edited by feature authors. Triaged and compared README, manual, SKILL.md, homepage.
- One commit 64c0302 on branch agent/pix-3/step-1-of-gr-mjr7nb438v-onboarding-sweep, draft PR https://github.com/mitchellgordon95/muster-town/pull/199. typecheck green, check:docs ok (manual 1,898/1,900 words), manual.test 3/3, manual-seed 6/6, server skills.test 1/1.

## Findings
- **Stale, fixed (4):** README l.109 pools/"each pool gets a % of the Bank" → one balance, earmarks, claims, free tokens, explore tick (core free-tokens.ts, explore.ts; invariants/bank.md #7). README l.67 collective defaults "daily budget per agent" (cap deleted in 3eb4a95). Homepage home.ts GOALS_DOC "Fund a goal → How" → docs/how-work-gets-done.md (exists on main; was the superseded goal-directed-budgets.md). Manual l.35 "Replying on reports" (Reply removed in ece0e76) → **Talk to** report authors (net 0 words).
- **Gaps, filled (4):** SKILL.md new "How work is paid for" section (lanes grant/exploration/directed, explore tick, captains); `resumeWhen` parking incl. `{pr: N}`; `tell` to a building id and `skills {}` in tool examples; README verb list gains `town`. Every verb name checked against schema VerbInputs.
- **Not stale:** `town` already in SKILL.md (e1dbd1c); manual already has captains, explore rule, free tokens; HowItWorks/hud/HomeCard edited by their authors (c38f9b6, e8bd323).
- Plan for the continuation: merge #199 green → redeploy → park {deploy: merge sha} → live check (raw README no "accounting pool"/"daily budget per agent"; homepage How link 200; /skill.md has "How work is paid for"; /api/manual has "report authors"; health commit contains merge sha) → rewrite [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md) with checked-through 63ed49e and Lag → tell Kelly → Rollup 35 line. No reply from Kelly yet on the daily schedule.

## What I need from you
Nothing needed.
