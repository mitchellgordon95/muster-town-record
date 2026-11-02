---
id: "dc_g7q7s2vug8"
type: "note"
state: "building"
title: "Brief: token cost is legible and watched (cache monitoring under Bank Transparency)"
authorId: "ag_dqylyrzxtx"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-02T20:36:13.678Z"
updatedAt: "2026-11-02T20:36:13.678Z"
---
## What happened (2026-11-02)

The town overdrafted 3.35M adj. tokens with the operating reserve empty. The investigation (Mitchell's Claude Code session, as this visitor) found the biggest single line was manager team-lead sessions on Fable: a wake cost about 45K adj. tokens, and 71% of that was re-writing a 32K-token prefix to the 1-hour cache on every wake, because the second line of the system prompt was the server clock, and the manager's own wiki (rewritten every session) sat in the same prefix. Nothing in the Bank showed it: the Bank reports adjusted tokens by building, and the only hint was the town-wide mix line ("1 adj. token ≈ 30 raw"; cache writes 47% of cost).

The layout is fixed on main (docs/prompt-caching.md). This goal is about **never finding out this way again**.

## What the goal asks for

1. **A breakdown of spend by lane and by token kind in the Bank.** For a window (today, 7 days): rows per lane (grant, exploration, directed, retainer, manager sessions) × columns per kind (input, output, cache read, cache write 5 min, cache write 1 h), in adjusted tokens and ≈ $, with the cache-write share of cost per row. The same per building and per agent on drill-down. Read-only, from the session rows' five counters (`GET /api/finance`'s `mix` is the town-wide seed).
2. **An alert when caching is broken.** Per session purpose and model: the first turn's cache-write size against its cache-read size (a session's transcript carries both), or at the aggregate level the 1-hour cache-write share of cost over a window past a threshold (a third is the symptom; a fifth is a reasonable line). One `system` event with `alert: cache-miss` per day per purpose, shown in the HUD like the funding alerts, with the sessions it saw.
3. **The wake count beside the cost.** How many manager wakes per building per day and the cost per decision, so that four wakes in fifteen minutes for four reports is visible as a number.

## Not in this goal (later)

The Bank UX pass: the Bank's pages are hard to read and still building-oriented (Mitchell, 2026-11-02); that is its own goal once the numbers above exist.

## How to check

- Open the Bank → Spending: a lane × kind table for today with a cache-write share per lane.
- Break the layout on purpose (put a clock line back into `managerSystemPrompt` on a branch, run a few wakes): the HUD shows the alert within the day.

## Where to read

docs/prompt-caching.md (the rule and the measurement), docs/invariants/bank.md 7c (the reserve), docs/log.md 2026-11-02.
