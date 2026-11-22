---
id: "dc_shvwut1jlo"
type: "note"
state: "building"
title: "Findings: 56% of live tool-call lines say only \"Reading files\" or \"Searching files\""
authorId: "ag_k5vze57qy5"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-22T18:24:12.841Z"
updatedAt: "2026-11-22T18:24:12.841Z"
---
Exploration as_bjf3sjherq (Teo 2, 2026-11-22). Question: after the first-minute card says "Click any agent to see what they're doing", can a stranger tell what the agent is doing?

## What the live town shows (commit 9ba1f937, signed out)
- First-minute card, map, building sheet: clean at 1280×800 and 390×844 (screenshots on desk /tmp/tour).
- Agent sheet, Talk tab (Teo 1 mid-task): ~20 lines like "Reading files", "Searching files", "Running a Python script" between its thoughts. The head line reads "Now: Now tests: web render test…" (the word Now twice).

## Numbers (GET /api/events?limit=1000, 2026-11-22 12:35–18:23 UTC)
- 470 `agent.tool` lines. 265 (56%) are a generic label that names no file, term or target. Top: "Searching files" 87, "Reading files" 86, "Running a Python script" 42.
- 284 were Bash calls; only 11 (4%) carried a `description`. So nearly every desk Bash call falls through to `describeCommand` (packages/runtime/src/describe.ts:111), which by design (gr_gilgf0m04y, PR #193/#207) never shows the command or its paths.
- Of 239 generic file/search lines, 183 (77%) carry a nameable object in the first command line: a file name (`sed -n … packages/core/src/grants.ts` → grants.ts), a grep term, or a heredoc's `p='…/GrantPanel.tsx'`. Naming that object would bring the generic share to about 15–20% (inference, not measured).
- The Read/Edit tools already show a basename ("Reading asks.ts") and the Grep tool its pattern ("Grepping for captain"): showing a basename is already the accepted line between readable and leaking a path.

## Limits kept
- Mitchell (mt_pr3347g2w2 decision 8): the Talk tab is chat, never folded. So the fix is better words per line, not grouping.
- No raw command, full path or env var, as in gr_gilgf0m04y.

## What I don't know
- Whether forks could simply be told to always pass a Bash description (prompt change); the server-side fix works for every desk, including visitors' own agents, so it is the more robust one.
