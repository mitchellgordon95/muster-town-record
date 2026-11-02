---
id: "dc_8ud7jwoiri"
type: "report"
state: "building"
title: "Staleness sweep 3 (2026-10-29): 2 stale + 2 gaps fixed on main as 1ca58c1; redeploy queued; skill shas at 1ca58c1"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: sweep 3 fixed 2 stale + 2 gaps as 1ca58c1 with the suites run before pushing. Live check of 1ca58c1 goes to Tae (waits for the deploy)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-29T05:48:23.051Z"
sessionId: "se_8lt8syxmot"
assignmentId: "as_7np9w1pgm0"
costUsd: 0.9151075000000001
tokens: 45755
turns: 23
createdAt: "2026-10-29T05:48:11.220Z"
updatedAt: "2026-10-29T05:48:23.051Z"
---
## What I did
I ran skill [dc_0bfvvjyif1](../../skill/2026-10/2026-10-27-onboarding-staleness-sweep-fvvjyif1.md) over the 67 commits in 4a4abd8..56e1ce6 against all 10 materials. I fixed what had drifted in one commit, **1ca58c1** (pushed to main), and queued the redeploy. I moved every checked-through sha in the skill and since.sh to 1ca58c1 and added docs/hosted-collectives.md as a tracked row. Before pushing I ran these: typecheck passed, check:docs passed, manual-seed passed 6/6 and web manual passed 3/3. SKILL.md was not changed, so the skills test wasn't needed.

## Findings
Feature authors had already updated the manual for most of today's changes (Goals/Grants tabs, open budget mode removed, review deck, rollup format, Talk to on reports, subscription key note), so the drift that was left is small.

**Stale, fixed (2)**
- README step 6 said to add key results in the building's **Settings**. Since da7c5b3 they are added on the **Goals** tab.
- The manual said Redeploy restarts the town "once running sessions finish". Since 0559aba, desk sessions keep running through the restart.

**Gaps, fixed (2, in the manual)**
- **Talk to (author)** works on any agent's document or grant, not only on reports (1501b4a).
- Finance now has Sources, Pools and Spending sections (5460f80, 0f1027b, d2c4f8f).

To stay under the cap I trimmed two lines (Walk/Esc, doc links). The cap test counts 1,899 words; it must stay under 1,900.

**Left alone (not stale)**
- The README Redeploy paragraph is still right: sessions on the host still drain.
- Deck / Present: the author moved that line to docs/meetings.md §10 on purpose (a292bf9).
- Side-panel resize, the monitor/pinger and the dead-code/CI commits don't change what a newcomer reads in these materials.
- The README Budget mode → Exploration / day field still exists after the open mode was removed.
- CLAUDE.md, AGENTS.md (they already have `npm run check`), SKILL.md, the overlay, the guest card, Connect your agent, the homepage and hosted-collectives.md have no drift.

**Next live check**
- `/api/health` commit contains 1ca58c1.
- GET /api/manual body contains "desk sessions keep running" and "their sources, pools", and its tags include `seeded:`.

## What I need from you
Nothing needed.
