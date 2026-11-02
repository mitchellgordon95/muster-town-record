---
id: "dc_800r2vqetc"
type: "report"
state: "building"
title: "Doc-drift ownership split with Code Legibility agreed (Mitchell's ask via Mara): Onboarding keeps meaning (daily sweep, KR 6), Mara's CI check owns mechanical references in README/CLAUDE.md/AGENTS.md, extended to SKILL.md and manual.md paths only; no code change"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_mu57k5t71o","dc_0bfvvjyif1","dc_obzzxrdxwr"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Split agreed and recorded (wiki dc_su3j6yz2s1); Craig's sweep 2 (queued 2026-10-28) folds the two rules into the skill. No code shipped, nothing for Mitchell; goes into the next rollup's Decided."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T06:31:16.513Z"
sessionId: "se_idreqfxppw"
assignmentId: "as_8i8naczycd"
costUsd: 1.0472005
tokens: 11171
turns: 10
createdAt: "2026-10-27T06:10:16.943Z"
updatedAt: "2026-10-27T06:31:16.513Z"
---
## What I did
Read Mara's note [dc_mu57k5t71o](../../../../bl_vd69s5a1nh/docs/note/2026-10/2026-10-27-doc-drift-vs-onboarding-copy-drift-who-owns-what-c-57k5t71o.md) and Craig's sweep skill [dc_0bfvvjyif1](../../skill/2026-10/2026-10-27-onboarding-staleness-sweep-fvvjyif1.md), replied to Mara with `tell` (ms_0a6jnemndi) agreeing to the split, and told Craig (ms_mr9t6gi28p) what to add to the skill in sweep 2. Cancelled the session the town auto-queued for Craig from that tell (as_3nbmq3b6ra; the message stays in his inbox, no action was needed now). Wiki page "Staleness sweep (KR 6)" dc_su3j6yz2s1 records the split. No code change; a redeploy was waiting on this session, so it ends here.

## Findings
- **Split agreed, by kind of check, not by file.** Onboarding (kr_hee2pa2d5r) owns *meaning*: is a claim in README/CLAUDE.md/AGENTS.md, the manual, SKILL.md and the web copy still true. Code Legibility (kr_oubxzkl4n6) owns a *mechanical* CI job that fails a PR or main run when README/CLAUDE.md/AGENTS.md name a file path, npm script, package or tool name that doesn't exist; it never rewrites prose. Design notes stay theirs. Mara's three no-collision rules stand as written.
- **Why it's the right split:** sweep 1's CLAUDE.md fixes (missing `desk` package, wrong `data/` and `export/` paths) are exactly what her check would have failed before the sweep saw them. The two checks are complementary, not duplicates.
- **Two caveats I attached:** (1) extend the check to skills/muster-town/SKILL.md now (paths and tool names; it is served to visiting agents), and to docs/manual.md for paths, scripts and packages only, never verbs, since the manual names UI buttons like "Ask to join"; CI covers only the repo copy, the live doc [dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md) can be hand-edited. (2) Onboarding pushes straight to main, so a red main run from one of our commits gets fixed the same day once she tells us; the daily sweep also picks it up.
- **Sweep skill changes for Craig's sweep 2** (queued for 2026-10-28, ≤100 k): a broken path/script/tool name found by the sweep is fixed as usual and reported to Mara with the pattern (no path check of our own); red main runs from our pushes are fixed that day.

## What I need from you
Nothing needed.
