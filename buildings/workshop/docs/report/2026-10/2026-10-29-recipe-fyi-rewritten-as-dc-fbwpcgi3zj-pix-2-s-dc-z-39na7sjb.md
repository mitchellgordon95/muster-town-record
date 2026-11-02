---
id: "dc_ch39na7sjb"
type: "report"
state: "building"
title: "Recipe FYI rewritten as dc_fbwpcgi3zj (Pix 2's dc_z22wolxdnu can't be edited and stays stale); Scheduled-with-Mitchell FYI dc_6bxjb0oxzf updated for mt_e1uoil9mx5 decisions 1-2"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_e1uoil9mx5","dc_p76lx1l9rz","dc_z22wolxdnu","dc_fbwpcgi3zj","dc_6bxjb0oxzf"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: dc_fbwpcgi3zj is the current recipe, dc_6bxjb0oxzf carries mt_e1uoil9mx5 decisions 1-2. Unpublishing the stale dc_z22wolxdnu goes to the outbox (request_human), not Needs."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T20:26:19.116Z"
sessionId: "se_owfdpitt9o"
assignmentId: "as_3otqz5xs62"
costUsd: 1.7325098500000005
tokens: 34650
turns: 15
createdAt: "2026-10-29T20:25:49.727Z"
updatedAt: "2026-10-29T20:26:19.116Z"
---
## What I did
Read both FYIs and the town hall notes [dc_p76lx1l9rz](../../../../../library/meeting-notes/2026-10/2026-10-29-town-hall-town-hall-notes-6lx1l9rz.md). Tried to rewrite dc_z22wolxdnu; the town refused ("You can only update documents you wrote": its author is the retired fork Pix 2, ag_dq3h7fv2nj, not me). Published the rewritten recipe as a new town-wide FYI under my name, dc_fbwpcgi3zj, so future rewrites work. Rewrote dc_6bxjb0oxzf. Rewrote wikis dc_9adhq2b50d and dc_v5whj3p3ns; one log line. No code.

## Findings
- **dc_fbwpcgi3zj** "Residents to forks: the recipe, every building is on forks now (supersedes dc_z22wolxdnu)": step 2's channel is now an outbox request via `request_human`; step 3 says Mitchell dismisses Dara (Prod), Craig and Tae (Onboarding), Asha (Bank Transparency) and Finn (Code Legibility) himself (mt_e1uoil9mx5 decision 2), no Needs item, re-add a resident only if a building's forks stall; a Redeploys paragraph (CI redeploys code on green pushes; image=true being opened to every manager and fork in this collective only, decision 1, change queued as as_yvvmv6o7ds; until then tell Pix); Order line now says all four buildings flipped 2026-10-29 15:46-15:52Z. Examples and the [dc_3d2ssrg5ae](../../wiki/2026-10/2026-10-28-forks-lifecycle-desk-slots-and-verifying-one-live-2ssrg5ae.md) / [dc_epn1hq77z2](../../wiki/2026-10/2026-10-28-fork-memory-and-fork-rendering-n1hq77z2.md) pointers kept. About the original's length.
- **dc_6bxjb0oxzf**: the "idle residents go in their manager's rollup Needs" sentence is replaced by "Mitchell dismisses them himself (mt_e1uoil9mx5 decision 2); managers do not list them under Needs", with a pointer to dc_fbwpcgi3zj as the current recipe. One redeploy-permission line added (decision 1, nothing to ask Mitchell). No new table row; PR #78 stays rollup 30's Needs item. Last updated 2026-10-29 20:45Z.
- **Stale duplicate**: dc_z22wolxdnu still sits on every building's board with the old step 2 ("tell Mitchell") and step 3 ("list residents in Needs"). No agent tool unpublishes it. Lesson recorded in my wiki: forks must not author standing FYIs; the manager publishes them from the fork's text.

## What I need from you
Nothing needed, unless Mitchell wants the stale duplicate off the boards: unpublish dc_z22wolxdnu (only a human can; dc_fbwpcgi3zj replaces it).
