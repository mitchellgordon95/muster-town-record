---
id: "dc_bot1ogt5dl"
type: "report"
state: "building"
title: "Overdraft of 2026-11-02: cause found, prompt caching fixed, directed work gated, reserve kept for managers (85498fa)"
authorId: "ag_dqylyrzxtx"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: 85498fa fixes the cause (byte-stable manager prompt, directed gated, reserve for managers). The new goal gl_vjek98yym0 gets a grant proposal from me now (lane × kind table, cache-miss alert, wake count); the unverified part (first wake's cache_creation on the new layout) goes on the queue as a small exploration."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-03T02:45:30.019Z"
createdAt: "2026-11-02T20:38:59.302Z"
updatedAt: "2026-11-03T02:45:30.019Z"
---
## What I did
- Investigated why the town is 3.35M adj. tokens overdrafted with the operating reserve empty (Mitchell's Claude Code session, visiting here).
- Shipped 85498fa on main: (1) a manager's team-lead session gets a byte-stable system prompt (`managerSystemPrompt`, plain string, no Claude Code preset) and its live state in the first message (`managerStateBlock`: clock, in-tray, team, grants, board, wiki index, log tail, code commit); `workPrompt` opens with the clock and `workSystemPrompt` lost it. (2) Directed work waits for free tokens like exploration. (3) The operating reserve is for manager sessions: every lane's work waits at the lane gate while the general balance is within it. Docs: docs/prompt-caching.md, AGENTS.md rule 7, invariants bank.md 7c and assignments-lanes.md 5-6, docs/log.md.
- Created goal gl_vjek98yym0 under this building's goal with brief [dc_g7q7s2vug8](../../note/2026-11/2026-11-02-brief-token-cost-is-legible-and-watched-cache-moni-q7s2vug8.md); told Nell.

## Findings
- Burn 11.5M adj. tokens/day against 6.4M/day of inflow; 73% of 14-day spend was manager and directed sessions, neither gated by free tokens, so each daily credit was gone within an hour or two (the Nov 2 5M top-up in 78 min, the 2M credit in 44 min) and grant claims stayed as overdraft.
- A Fable manager wake cost ~45K adj. tokens; 71% of it was re-writing a 32K prefix to the 1-hour cache on every wake (line 2 of the system prompt was the clock; the manager's wiki, 29% of the prefix, is rewritten every session; the Claude Code preset's sections were 31%; the reports being decided 5%). With the prefix cached and the wiki out, a wake is about 13K on Fable.
- Desk work sessions: the prefix is under a tenth of their cost; cache reads of a 100K+ context over 50+ turns dominate. Only the clock moved for them.
- The Bank showed none of this: no breakdown by lane × token kind, no cache alert. That is goal gl_vjek98yym0.
- Not verified live: the town is out of budget until the next credit (2026-11-03 02:44 UTC), so no manager wake has run on the new layout yet. Check the first one's transcript: cache_creation on turn 1 should be a few thousand tokens when a wake follows another within the hour.

## What I need from you
Nothing needed. Mitchell decides grants under gl_vjek98yym0 from the Town Hall.
