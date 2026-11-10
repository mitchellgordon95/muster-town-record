---
id: "dc_b4musn05et"
type: "wiki"
state: "building"
title: "Ask card lint decision (style warns, structure refuses)"
authorId: "ag_wqa7t10gqd"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-10T19:28:48.945Z"
updatedAt: "2026-11-10T19:36:12.516Z"
---
State 2026-11-10 after as_s9t0vysjnd (Pix 2). Source: 1:1 mt_ewxnhs90cq decision 5 (Mitchell 18:58 "i don't think we need the linter for text", 19:08 "let's document the lint decision"). Build report [dc_ipwfu68yfy](../../report/2026-11/2026-11-10-lint-decision-ask-style-rules-are-warnings-only-mi-wfu68yfy.md).

- **PR #412 MERGED** to main as dc437530 (CI green: check + image; main had not moved, no migrations). Not yet confirmed live: CI deploys it; check /api/health commit contains dc437530.
- Refused every time (no retries): <2 branches, empty recommendation field, hard contract fields (money prior-decision/spent/steps; click parked; credential scope+fallback; meeting question; policy rule). Code: schema ask.ts `askStructure`, core asks.ts `refuseMissingStructure`.
- Warnings only (lint history entry "warnings: …", named in the answer of submit_report / propose_grant / calibrate): every ASK_LINT_RULES style rule + soft contract fields (money claims, click permission, policy what-I-did / reversing cost). Code: `askWarnings`.
- Gone: refuseOrFlag, ASK_STRIKES, ask.refused events, lint-failed tag (legacy tags dropped on rewrite) and the AskCard pill.
- Prompt (prompts.ts askCardRules): style listed as not refused + active voice + dictionary words.
- Docs: legible-delegation.md §12 q4 decided; invariants/asks.md #8.

