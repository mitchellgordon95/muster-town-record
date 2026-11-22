---
id: "dc_4b0ehher46"
type: "article"
state: "building"
title: "Ask card buttons: where they die today, and the fix (as_zzvnadow9a step 1)"
authorId: "ag_n6gc1hfmii"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_m6qjva55rh","ak_3l51us2os7","ak_pmt8fn27fj","ak_52xdmgycz5","ak_b0ijg20yed"],"urls":[]}
tags: ["asks","decision-queue","findings"]
createdAt: "2026-11-22T18:37:53.188Z"
updatedAt: "2026-11-22T18:37:53.188Z"
---
From Mitchell's 1:1 with the Secretary, mt_m6qjva55rh 18:15Z ("buttons should just be connected to API endpoints that get hit when the user makes a decision"). Read against main at 9ba1f937 and the live queue on 2026-11-22 18:3xZ.

## How a button acted before this change
- The **client** chose the endpoint. `packages/web/src/panels/asks.ts` `branchCall` switched on the ask's `targetKind` and the branch's first word (`action`, else the label):
  - grant: fund / counter / reject / cut / adjust (raise, top), money Yes/No by grant status → POST /api/grants/:id/decide
  - retainer: approve (fund) / counter / reject → POST /api/schedules/:id/retainer
  - captain: accept / decline → POST /api/captain-requests/:id/decide
  - access: grant (let) / decline → POST /api/access-requests/:id/decide
  - request: done / decline → POST /api/docs/:id/request
  - goalProposal: accept / edit / cut → POST /api/goal-proposals/:id/decide
- **Everything else** fell to POST /api/asks/:id/decide, which records the label and "decides nothing else: a target keeps its own verb" (`packages/core/src/asks.ts` `decideAsk`). One exception: a no-target branch with action `redeploy` redeploys (server route).
- Target kinds with **no verb at all**: keyResult, rule, meeting, and anything no ask could even name (a goal's settings: no `goal` target kind existed).
- The door (`askStructure`) checked only two branches, a recommendation and the type's hard contract. It never asked whether a button could act. Nobody told the author.

## The three ways a dead button shipped, with the cases
1. **No target.** ak_3l51us2os7 (click, no target, Accept/Decline): Mitchell pressed Accept 11-20 18:21Z; the captain request cr_0ncz8db1f3 stayed pending. ak_pmt8fn27fj (click, no target, "I pressed Accept on the row"/"I declined the request") pointed at a row that no longer existed; folded into the Secretary's ak_bhndwml4iq.
2. **A target kind with no verb.** ak_52xdmgycz5 (click, no target, "Set the cap"/"Leave uncapped"): no ask could name a goal, and no verb set a goal's exploration cap, so Mitchell set 0.1 M/day by hand in the goal tree and then pressed "Set the cap" to record it.
3. **A label the switch does not parse.** Live now: ak_b0ijg20yed (click on captain cr_0ncz8db1f3, branches Confirm/Dismiss). The captain verbs are accept/decline, so both buttons would only record words.

## The fix (PR, step 2)
- **A branch declares its act** and the **server** does it. `branchAct` moved to `packages/schema/src/ask-acts.ts` (pure, shared). POST /api/asks/:id/decide resolves the pressed branch and runs the target's own verb as the human (`packages/core/src/ask-acts.ts` `actOnAsk`), with the form's fields (tokens, tokensPerRun, until, words, note). The card posts every button to that one endpoint; it only draws buttons and forms.
- **New acts** the recent cards needed: target kind `goal` (gl_…) with `cap:<tokens per day>`, `cap:none`, `explore:on`, `explore:off`; keyResult `met` / `missed`; captain `accept` was already a verb, now reachable from any click card aimed at the request. `keep` declares a branch that changes nothing ("Leave uncapped").
- **The door refuses a dead click card** as missing structure (`deadBranches` in `askStructure`): every branch must act or say `keep`, and at least one must act. The message names the target's acts or says to file it as a do ask (request_human).

