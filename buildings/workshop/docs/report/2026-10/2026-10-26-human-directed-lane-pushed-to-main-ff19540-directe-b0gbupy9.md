---
id: "dc_tkb0gbupy9"
type: "report"
state: "building"
title: "Human-directed lane pushed to main (ff19540): directed work cites a human source and never uses the exploration allowance; parked for live check"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved; the parked continuation does the live check of ff19540. When it's live, tell me and I'll re-lane as_cwg8ctj1cx and as_9mm7ee38eb as directed (sources: 1:1 mt_ryw7ejayvu decisions)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T23:31:33.810Z"
sessionId: "se_005sabb57l"
assignmentId: "as_ockmoi2uad"
costUsd: 0.7275898999999999
tokens: 32739
turns: 20
createdAt: "2026-10-26T22:41:25.854Z"
updatedAt: "2026-10-26T23:31:33.810Z"
---
## What I did
Rebased my earlier unpushed patch (dcf34f6) onto current main. Its migration number had collided with another one, so it is now 038_assignment_source.sql. I resolved the conflicts with Bank step 3: the directed bucket is now summed in adjusted tokens, and /api/health shows `accounting` and `budgets` side by side. I also fixed the new "done" hold so it fits main's newer blockers shape. Pushed to main as **ff19540** and asked for a redeploy. ff19540 should be live after the restart; it is not verified live yet.

## Findings
- **The rule:** `assign`, `review` continue/redirect and meeting decisions can now name lane `directed` with `sourceId`. The source must be human: a meeting a human took part in (or its notes), a doc a human wrote (a flag or human-report), a report or rollup a human decided with a reply note, or a human's tell. The check is `humanSource` in `packages/core/src/lanes.ts`. Without a human source, agents get the old error text, "…; agents can't create directed work".
- **The directed bucket:**
  - The exploration allowance never holds directed work.
  - Its spend is counted in its own bucket: `grantDesk.directed`, and `budgets[]` in GET /api/health (each goal-directed building's exploration allowance/spent and directed spent).
  - It also appears as "Directed today" in the Key results block, and as today's spend by lane in the manager rollup template.
- **Stop condition:**
  - Directed work that names a keyResultId is held once a non-draft, non-rejected grant proposal names that KR. The blocked view shows it as "done: grant proposal X names its key result".
  - Assigning directed work to a KR that already has a proposal is refused.
  - A **gap** has no automatic stop, because grants can only name KRs. Gap work runs until its own report ends it.
- **Docs and prompt:** the lanes section of `docs/goal-directed-budgets.md` is updated. The manager prompt no longer says "You can't create directed work"; it explains `sourceId`.
- **Checks:**
  - Core, server and web typecheck clean.
  - `lanes.test.ts`, `v12.test.ts` and `blockers.test.ts` pass (25 tests), including 3 new ones: source validation and the bucket, meetings with or without a human, and the KR stop.
  - I did not run the full suite.
- **Still open:** Pix re-lanes as_cwg8ctj1cx and as_9mm7ee38eb after the live check. I'll tell Pix when I resume.

## What I need from you
Nothing needed.
