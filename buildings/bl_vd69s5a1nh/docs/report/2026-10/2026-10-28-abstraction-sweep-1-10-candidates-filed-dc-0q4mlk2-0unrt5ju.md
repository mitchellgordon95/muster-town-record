---
id: "dc_a90unrt5ju"
type: "report"
state: "building"
title: "Abstraction sweep 1: 10 candidates filed (dc_0q4mlk2wuh)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_0q4mlk2wuh"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good sweep: 10 ranked candidates with file:line, drift called out, Bank-touching sites fenced off. Proposing a grant for kr_doa59kdway on candidates #1, #2, #3 (server sites), #7 as a fourth."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T17:40:30.895Z"
sessionId: "se_n1wd5kivb8"
assignmentId: "as_8j4xpiacul"
costUsd: 1.8095706999999999
tokens: 90479
turns: 43
createdAt: "2026-10-28T17:37:18.531Z"
updatedAt: "2026-10-28T17:40:30.895Z"
---
## What I did
Swept `packages/` at main 6af7714 for repeated code outside the core subsystems. I used targeted greps plus a small duplicate-window detector I wrote (`/home/agent/tools/dupes.py` on my desk). I filed the ranked candidates as [Abstraction sweep 1: candidates](../../note/2026-10/2026-10-28-abstraction-sweep-1-candidates-4mlk2wuh.md). The town's `write` tool refuses type "report", so the doc is a note in the filing cabinet; it is still citable in findingsDocIds. Nothing was consolidated, no code changed and there is no PR. Wiki page "Abstraction sweeps" is written.

## Findings
There are 10 candidates, each with file:line for every occurrence, the proposed abstraction, risk and a token estimate. Three of them are copies that have already drifted apart.

**Top 3, ~105k tokens in total:**
1. **Desk contract → schema** (~40k tokens). `desk/src/contract.ts` copies 5 schemas from `schema/src/index.ts:1585-1653`, and the file's own TODO asks for this switch.
   - Drift: the server sends `interrupts[].now` (`server/src/routes/desk.ts:60`), but the schema's `DeskControl` doesn't declare it, so anything parsing with the schema loses it.
2. **SQL WHERE builder `whereOf` in `core/src/table.ts`** (~35k tokens). It replaces 7 hand-rolled `where.push`/`params.push` sites in events, grants, skills, verbs/docs and routes/docs.
3. **`permissions.requireAdmin` / `isUserAdmin`** (~30k tokens). It replaces 12 `isAdmin({kind:"user"…})` checks with hand-written 403s. Three of them are in `core/bank.ts`; leave those out until Mitchell OKs them.

**The rest:**
4. `desk/src/sdk.ts` is a ~110-line copy of `runtime/src/sdk.ts`, the largest duplicate in the repo. It has drifted: the desk's `LooseMessage` has an `error` field the runtime's lacks. The code is token accounting, so ask Mitchell before moving it.
5. Three separate town HTTP clients (CLI, web, desk). They handle errors differently, and none sets a request timeout.
6. 13 response view types are hand-copied in `web/src/api.ts`; most are Bank types.
7. `DAY_MS` and day-string math is repeated about 15 times.
8. The web map editors (`layoutEdit.ts`, `townPlan.ts`) repeat the same debounced draft-preview store.
9. The SDK message-stream loop exists in three places. Host and desk sessions classify errors and spend-limit deaths differently. I haven't checked whether host sessions miss `bank.cap` events; this one is high risk.
10. Small web formatting copies.

Candidates 1–8 total ~295k tokens. All estimates are ±50%.

## What I need from you
Nothing needed. To be precise, no commit of mine is waiting on the pending redeploy.
