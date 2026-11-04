---
id: "dc_o6tckqg5i3"
type: "report"
state: "building"
title: "Secretary grant proposed: gr_kdlogzzo5s (900k, 4 KRs), design dc_8gbluwrdgi"
authorId: "ag_20uo6cja1v"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_v09cn7a8yr","dc_8gbluwrdgi"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done as assigned: gr_kdlogzzo5s (900k, 4 KRs) proposed on gl_join, design dc_8gbluwrdgi filed. Mitchell decides it in the Town Hall in-tray; it folds into the next rollup."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T02:47:24.408Z"
sessionId: "se_yfllvxbqw3"
assignmentId: "as_cj1pde5t3n"
costUsd: 0.78175
tokens: 39088
turns: 18
createdAt: "2026-11-04T02:46:19.205Z"
updatedAt: "2026-11-04T02:47:24.408Z"
---
## What I did
Read the core code on main 7e439b3: grants.ts (decide/stop/canFund/history), meetings.ts (1:1s), retainers.ts, schedules.ts, review-deck.ts, schema rollup.ts, and runtime manage.ts. Wrote the design doc [dc_8gbluwrdgi](../../article/2026-11/2026-11-04-design-the-secretary-a-town-hall-resident-with-a-d-bluwrdgi.md) and proposed gr_kdlogzzo5s. I built nothing.

## Findings
- **Proposal gr_kdlogzzo5s** (goal gl_join, asks 900,000 tokens). Its key results:
  - kr_spolcs3akx (due 11-10): a digest card is the first thing in the Town Hall in-tray. It has "Decisions needed" as yes/no lines, then "Shipped since last digest" with one line and picture per item. The rollups it covers sit under it, and it is also a deck slide.
  - kr_rl8l0xfrkm (due 11-10): the digest runs on an approved daily retainer, only when new rollups have arrived. The Secretary runs it, not a fork of the Planner.
  - kr_nt0q4a3pmy (due 11-11): a decision Mitchell speaks in a 1:1 with the Secretary is applied and recorded in the grant's history as "by Mitchell via Secretary in mt_…", quoting his words.
  - kr_sdtzgbyrxn (due 11-09): tests show that only recent words from the 1:1's own human count, the human's own permission check applies, and stop and Bank inputs are refused.
- **How the 1:1 actions stay narrow:** add one new verb, `act_in_1on1`. The agent must be the 1:1's facilitator and must cite the human's own utterance from the last 30 minutes. The verb then calls the existing `Grants.decide` / `decideRetainer` with **the human as the actor**, so the same `canFund` / `canDecideRetainer` checks apply. The Secretary can never do anything the human couldn't. Stopping a grant stays a button. **No Bank or token-accounting change is needed.**
- **One schedule change is needed:** `scheduleTaker` (schedules.ts l.197) always forks the building's manager. The Planner has no forks, so schedules need an optional `takerId` for the Secretary to take the digest job.
- **Sizing:** the town's estimate line was "3 similar grants spent 77,238–1,201,832; this building spent/funded 0.98". I asked for 900k, above the 750k that gr_8i952perny needed after its top-up, because this grant has more parts. The note to Mitchell says why.

## What I need from you
Nothing needed. The proposal reaches Mitchell through the in-tray.
