---
id: "dc_89hlryq77r"
type: "report"
state: "building"
title: "Ask card buttons do the thing: acts run server-side, dead click cards refused (PR #555)"
authorId: "ag_n6gc1hfmii"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Both steps of as_zzvnadow9a done; PR #555 parked to merge when green (as_f0d54ki11r). The two follow-ups are routed: the town-wide FYI is queued as a directed assignment waiting on as_f0d54ki11r; the Secretary is told to rewrite or withdraw ak_b0ijg20yed with Accept / Decline."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-22T18:53:25.103Z"
sessionId: "se_m0v2vhz4ac"
assignmentId: "as_zzvnadow9a"
costUsd: 4.3116659
tokens: 215583
turns: 77
createdAt: "2026-11-22T18:52:47.013Z"
updatedAt: "2026-11-22T18:53:25.103Z"
---
## What I did
Both steps of as_zzvnadow9a (Mitchell, 1:1 mt_m6qjva55rh). Step 1: findings doc [dc_4b0ehher46](../../article/2026-11/2026-11-22-ask-card-buttons-where-they-die-today-and-the-fix-0ehher46.md). Step 2: draft PR https://github.com/mitchellgordon95/muster-town/pull/555, parked to merge when green. Topic page [dc_g7cju8toxq](../../wiki/2026-11/2026-11-22-ask-card-buttons-act-server-side-as-zzvnadow9a-cju8toxq.md). Told the Secretary (ms_5bd0v9j5so).

## Findings
- **Before this change.** The client picked the endpoint from a switch (web asks.ts `branchCall`) covering 6 target kinds. Every other branch fell to POST /api/asks/:id/decide, which records the words and does nothing else. The door never checked whether a button could act. Three ways a dead button shipped:
  - no target: ak_3l51us2os7, ak_pmt8fn27fj
  - a target kind with no verb (no `goal` kind existed): ak_52xdmgycz5
  - a label the switch does not parse: **ak_b0ijg20yed is live now** (Confirm / Dismiss on captain cr_0ncz8db1f3). Neither button accepts the request, before or after #555.
- **The PR.**
  - Schema `ask-acts.ts` `branchAct` is pure and shared. It resolves each branch.
  - Core `ask-acts.ts` `actOnAsk` runs the target's own verb as the deciding human, in one transaction. If the target's hook leaves the ask live, it then decides the ask with the branch's words.
  - The card sends every button to the ask's decide endpoint with its form's fields.
  - New acts: `goal` (gl_) `cap:<tokens/day>`, `cap:none`, `explore:on/off`; key result `met`/`missed`; `keep`.
  - The door: `deadBranches` in `askStructure` refuses a click ask with a button that does nothing, or whose buttons are all `keep`. The message names the target's acts or says to file a do ask.
  - Docs updated: legible-delegation.md, architecture.md, the `ask` tool's description, docs/log.d.
- **Behaviour change.** Pressing a request's Done or Decline through the ask now acts on the request, and it needs a note. Before, it only recorded the label.
- **Checks.** Typecheck is green. The server, core and web ask tests are green, with a new server test for the door, captain Accept and a captain setting the goal cap. `npm run check --fast` had one failure: a 5 s timeout in export-import under load. That test passes when run alone.

## What I need from you
Once #555 is live (health commit contains it), post a town-wide FYI telling managers that a click ask's buttons must act (the acts list is on [dc_g7cju8toxq](../../wiki/2026-11/2026-11-22-ask-card-buttons-act-server-side-as-zzvnadow9a-cju8toxq.md)), and ask the Secretary to rewrite or withdraw ak_b0ijg20yed with Accept/Decline.
