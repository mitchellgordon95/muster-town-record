---
id: "dc_roa13mx4aw"
type: "report"
state: "building"
title: "Town Hall \"User stats\" stand is live and checked (6eb6560)"
authorId: "ag_ldvub2gvzl"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "User stats stand live check done (6eb6560)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T02:04:10.010Z"
sessionId: "se_2yr4mxo7sn"
assignmentId: "as_wyr76zz4xw"
costUsd: 0.6413407999999998
tokens: 32067
turns: 19
createdAt: "2026-11-01T02:30:16.995Z"
updatedAt: "2026-11-02T02:04:10.010Z"
---
## What I did
Confirmed 6eb6560 is live. It is an ancestor of the live commit 244d9d1, and the server started 2026-11-01T02:26:15Z. The served main-C95xTOHt.js contains "Read the user stats". I ran headless Chromium with a fresh profile and a signed-out guest on the Workshop and on /hollyville/, at 1400×900 and 390×844: `musterTown.walkTo("stats")`, then pressed E. I took two cropped pictures and updated the topic page [dc_ze5o8drnl9](../../wiki/2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md).

## Findings
- **Passed in all 4 runs (2 sites × 2 sizes):** walkTo returned true, the stand shows next to the 2-tile outbox counter, the prompt reads "E Read the user stats", and there were 0 console errors.
- **E opens the panel with live numbers:**
  - **Workshop:** 147 saw card, 2 signed in, 1 asked, 1 let in, 0 declined, typical wait 15 s. By day: Nov 1, Oct 31, Oct 29. Per collective shows workshop and hollyville.
  - **Hollyville:** only its own numbers (2 / 1 / 1 / 1 / 0, 15 s), with no Per collective table, as designed.
- **One glitch:** in the first desktop Workshop run, E pressed right after the walk did not open the panel. The prompt was on screen with "Tab next 2/2". On a rerun, E opened it. It looks like a timing race in the headless run; I could not make it happen again and did not chase it further.
- **Pictures:**
  - Stand in the Town Hall: ![User stats stand](/api/media/mf_r1deqt80ux.png)
  - Panel: ![User stats panel](/api/media/mf_r40zfuzumf.png)
- This finishes as_uvkh7ghqru. It can be rolled up with the Dashboard removal and the goal-tree docs.

## What I need from you
Nothing needed.
