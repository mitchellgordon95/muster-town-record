---
id: "dc_vhlqmanl0m"
type: "report"
state: "building"
title: "Mara's doc-drift check acknowledged (Mitchell's ask via Mara): draft PR #58 `npm run check:docs` matches the agreed split, not in CI until a human adds the workflow step; Craig told to run it before sweep pushes and to send Mara bare relative paths like `data/`; no code change"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_mu57k5t71o","dc_su3j6yz2s1","dc_0bfvvjyif1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/58"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: PR #58 matches the agreed split; the CI step is Code Legibility's need. Folds into the next Onboarding rollup as KR 6 context alongside dc_800r2vqetc."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T07:00:22.271Z"
sessionId: "se_q8ogdfaa1f"
assignmentId: "as_or8d14kq43"
costUsd: 1.3654108999999999
tokens: 10781
turns: 11
createdAt: "2026-10-27T06:59:50.457Z"
updatedAt: "2026-10-27T07:00:22.271Z"
---
## What I did
Read Mara's note [dc_mu57k5t71o](../../../../bl_vd69s5a1nh/docs/note/2026-10/2026-10-27-doc-drift-vs-onboarding-copy-drift-who-owns-what-c-57k5t71o.md) and her draft PR https://github.com/mitchellgordon95/muster-town/pull/58 (scripts/check-doc-refs.ts, `npm run check:docs`, 4 files, +132). Replied to Mara (ms_hq5rrhb9js). Told Craig (ms_ep33n4hnmf) two additions for the sweep skill [dc_0bfvvjyif1](../../skill/2026-10/2026-10-27-onboarding-staleness-sweep-fvvjyif1.md) in sweep 2 (queued 2026-10-28 ~06Z): run `npm run check:docs` locally before a sweep push to main, and send Mara any bare relative path the sweep finds. Rewrote wiki dc_su3j6yz2s1. No code, nothing shipped.

## Findings
- The check matches what we agreed: README/CLAUDE.md/AGENTS.md and skills/muster-town/SKILL.md are checked for paths, npm scripts, verbs, mcp__town__ tool names and CLI commands; docs/manual.md for paths and scripts only (no verbs, it names UI buttons). Mara says it passes on today's docs and deliberate breaks fail it.
- It is not in CI yet. The desk token can't edit .github/workflows, so a human must add the one-line step to the workflow. Until then Onboarding's direct pushes to main are not gated; hence the local-run rule for Craig.
- Known gap: only paths starting at the repo root are checked, so a bare `data/` (sweep 1's pattern) is not caught. Rule stands: the sweep fixes it and tells Mara the pattern; no path check of our own.
- The CI step is Code Legibility's need, not ours; it belongs in Mara's rollup. I'll mention it in our next rollup only as context for KR 6.

## What I need from you
Nothing needed.
