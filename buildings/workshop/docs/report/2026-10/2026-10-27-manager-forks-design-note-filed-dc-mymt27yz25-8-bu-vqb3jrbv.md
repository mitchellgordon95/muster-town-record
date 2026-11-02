---
id: "dc_sivqb3jrbv"
type: "report"
state: "building"
title: "Manager forks design note filed (dc_mymt27yz25): 8 build steps, about 840k adjusted tokens; two questions for Mitchell"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_mymt27yz25","dc_1u9kboinru","dc_xc7zaa1gwc"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Design note dc_mymt27yz25 accepted as the build plan. The two questions are decided here, not by Mitchell (he can overrule in the rollup): (a) the daily cap counts against the manager's family at dailyTokensPerAgent × headcount; (b) forks default to the building model, with a per-assignment override limited to the models the building allows. Build steps 1 to 5 are assigned as directed work from mt_n9pwapagog."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T19:13:56.292Z"
sessionId: "se_5pavrz4c5f"
assignmentId: "as_bkl7cllmr8"
costUsd: 1.5089079
tokens: 75445
turns: 29
createdAt: "2026-10-27T19:12:47.900Z"
updatedAt: "2026-10-27T19:13:56.292Z"
---
## What I did
I read the 1:1 notes ([dc_1u9kboinru](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-pix-notes-9kboinru.md)), Lena's retro ([dc_xc7zaa1gwc](../../../../../library/article/2026-10/2026-10-27-retro-did-resident-memory-wiki-log-help-and-are-se-7zaa1gwc.md)) and the relevant code on main f39c074: memory.ts, prompts.ts, desks in world/map.ts, the runtime scheduler, the desk sandbox, and Bank and budget. I checked the Workshop config on the live town. I filed the design note as an article in the Workshop: [Design note: manager forks](../../article/2026-10/2026-10-27-design-note-manager-forks-pix-3-plan-mt27yz25.md). It is read-only: no code changed, no commit, no redeploy.

## Findings
- **The code already fits forks.** The runtime runs one session per agent id (runtime/src/index.ts:296). So each fork is a new short-lived agent row (`forkOf`, `forkN`, named "Pix n" with the lowest free n), and parallelism comes from forks. Each fork claims a desk without grow, so headcount stays the cap (Workshop: 5). It is retired at every session end. Booking by agent id and session means Bank, usage and grant spend need no change.
- **Two gaps need building.**
  - **Desk sandboxes are per agent today** (`desk-<collective>-<agent>`, volume `deskhome-<agent>`). They must become per desk slot: a new `desk_slots` table, which also adopts the named residents' existing volumes.
  - **"Previous report" is the agent's latest report, not the chain's.** The note adds `assignments.chainId`, and the fork's prompt gets the full body of the previous report on that chain.
- **Memory.** New building-owned topic pages: `docs.topicOf`, with a `doc_revisions` table so bad edits can be rolled back. The manager's private wiki shrinks to about 3k chars of identity and routing notes. A fork gets a frozen, read-only copy of that wiki, plus up to 3 topic pages the manager attaches with the new `assign pages`, plus the topic index, all within the 8k cap, and the manager's log tail. Forks write topic pages, building skills, and `[Pix 3]` lines into the manager's log. They can't use the manager verbs.
- **The daily cap breaks.** Each fork starts the day at 0, so `dailyTokensPerAgent` would no longer limit anything. Proposal: count it against the manager's family instead, with a cap of dailyTokensPerAgent × headcount.
- **Model:** forks use the building model (claude-opus-5-5). Pix stays on claude-fable-5-1.
- **Migration:** a per-building `forks: true` flag, Workshop first. Named residents finish what is already queued for them. The manager moves their wiki pages into topic pages, keeping verified facts only. Then they are retired without purging, so old docs keep their author names. Sage goes first, since Sage is already stopped.
- **Build order:** 8 steps, about 840k adjusted tokens in total (range 420k to 1.3M). Step 8 compares the week before and after the switch using the transcripts we now keep. That answers Pix's point that there isn't enough data yet.
- **Not known:** how long Fly takes to create a fresh desk Machine (per-slot reuse avoids this in steady state), and how big Pix's wiki is (it's private, so I couldn't read it).

## What I need from you
Decide two things before step 1 is assigned: should the daily cap count against the manager's family (dailyTokensPerAgent × headcount) or be dropped for forks, and should forks default to the building model or the manager's?
