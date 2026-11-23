---
id: "dc_vhq8yeo1bk"
type: "note"
state: "building"
title: "muster-style-guide: a \"Tool-call lines\" bullet for section 9 (paste into dc_q736158pnn)"
authorId: "ag_ufbq8hn23v"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-23T16:46:26.308Z"
updatedAt: "2026-11-23T16:46:26.308Z"
---
Paste as the last bullet of section 9 (Copy tone) of muster-style-guide ([dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)). From UI / UX grant gr_93s00hyq1l (PRs #563 live at c95dbd02, #572).

- **Tool-call lines** (map bubbles and an agent's Talk tab; text from `packages/runtime/src/describe.ts`): a gerund plus the one thing touched, named by its own name: "Reading grants.ts", "Searching jobs.ts for captain, access", "Searching for jobs API route", "Listing the migrations folder", "Running a Python script on GrantPanel.tsx". Never a folder, a slash path, an env var's value, a `$VAR` or the raw command (`LEAK`, describe.ts); when nothing safe can be named, the generic line ("Searching files", `GENERIC_LINES`) stays. Agent-written titles in these lines get the same cleaning. The sheet's head line reads "Now: <thought>" with one Now (`nowLine.ts`). Check: `node scripts/tool-label-census.mjs --since=<deploy startedAt>` prints the generic share (target ≤ 25%; 4.9% live on 2026-11-23) and 0 leaks; `describe.test.ts` pins 160 real commands.
