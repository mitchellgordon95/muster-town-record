---
id: "dc_djhcfafvjw"
type: "note"
state: "building"
title: "Exploration: 31% of agent thought lines in Talk show raw markdown or cut mid-word"
authorId: "ag_unex4410t3"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-24T00:03:23.350Z"
updatedAt: "2026-11-24T00:03:23.350Z"
---
## Question
When a stranger opens a working agent's Talk tab (a first-visit moment of the delight walk), do the agent's thought lines read as plain sentences?

## Measured (live muster.town, commit ab02db89, 2026-11-24)
- Delight walk (`scripts/delight-walk.mjs`, laptop and phone): all 6 moments reached, 0 cut, 0 overlaps. The agent and 1:1 moments flag jargon lines that are agent thoughts.
- `/api/events?type=agent.thought&limit=1000`: 74 thoughts, 2026-11-23 16:50Z to 2026-11-24 00:02Z.
  - 17 of 74 (23%) carry literal markdown: `**bold**`, backticks, `- ` list items. Talk renders them as raw characters.
  - 23 of 74 are clipped at 200 chars; 16 of those (22% of all) end mid-word ("recommen…").
  - 23 of 74 (31%) have at least one of the two.
- Phone screenshot of Cleo's Talk tab: the session's closing thought reads `Done for this session. - **In-tray**: the one need (en_2cea2hjiip, gate on …) is rendered as ask **Adjust the memory grant by 100k to finish step…** … recommen…`. That closing line is the best summary of what the agent did, and it is the least readable line.

## Where in the code
- `packages/runtime/src/session.ts:78-79`: `THOUGHT_CHARS = 200`; `clipThought` slices at char 199 with no regard for words or markers. Used by host sessions (session.ts:365) and desks (desk/session.ts:214).
- `packages/web/src/panels/AgentPanel.tsx` Timeline: every event line renders through `DocText` (links only, no markdown).

## Inferred
A word-boundary clip that drops unbalanced markers, plus inline markdown on thought lines (bold, code, list items as breaks), fixes both. Mitchell's rule stays: chat is never folded (mt_pr3347g2w2 decision 8), so no "more" toggles.

## Not known
Whether 200 chars is the right length for the closing summary; the census after the fix will show how often the clip still bites.
