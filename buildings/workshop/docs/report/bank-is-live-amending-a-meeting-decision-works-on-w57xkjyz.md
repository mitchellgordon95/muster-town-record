---
id: "dc_xuw57xkjyz"
type: "report"
state: "building"
title: "Bank is live; amending a meeting decision works on the live town"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T19:59:27.108Z"
sessionId: "se_rsk7lglzqn"
assignmentId: "as_jhp28kzq4h"
costUsd: 0.5525684
tokens: 914438
turns: 27
createdAt: "2026-10-20T19:54:38.520Z"
updatedAt: "2026-10-20T19:59:27.108Z"
---
## What I did
I triggered the redeploy (image=false). From the server's event log I confirmed the Bank commits are live. Then I amended a real decision on the live town: in the standup (mt_ky5ci3qn22), during the 5-minute window after close, I replaced decision 1 (my own) with decision 5. I changed no code, so there is no commit or PR.

## Findings
- **The Bank is live.** Lena's redeploy at 19:49 UTC pulled the 4 Bank commits (663fa61..8842a21) and restarted the server. `/api/town` now has the `bank-map` place. My redeploy at 19:53 pulled 0 commits and rebuilt the client. It is now draining, waiting for the running sessions to end. It brings in nothing new, so the restart is harmless. Root's message assumed the earlier run stopped at 4f61fdf, but it didn't.
- **Amending a decision works on the live town:**
  - Decision 1 now shows `supersededBy: 5`, and decision 5 shows `supersedes: 1`.
  - Both keep the same assignment (`as_jhp28kzq4h`). No second assignment was created: it was rewritten in place, with a new title and a description ending "(amended; replaces: …)".
  - Because I was already working on it, I got the system message "Your current assignment was amended in meeting …".
  - The meeting notes (dc_ev7qckfr1h) gained a section "Decisions recorded after close", with "(replaces decision 1) …".
- **Small cosmetic gap:** when a decision is amended after the meeting closes, decision 1 is not struck through in the notes' original numbered list. The added line says what it replaces, so I left it.

## What I need from you
Nothing needed.
