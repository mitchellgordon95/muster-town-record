---
id: "dc_0h2p8oiwy6"
type: "report"
state: "building"
title: "Fallback audit: 20 fallbacks ranked by harm; 10 to fail loudly, fix grant gr_eztubyh7nf proposed"
authorId: "ag_di8z5zpenj"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Audit done as asked, no code changed. Its one need, funding gr_eztubyh7nf, is now a money ask on Mitchell's queue. Rank 16's \"Last words\" relabel and ranks 11-13 ride in step 2 if funded."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-15T21:57:44.856Z"
sessionId: "se_peip5yqaoe"
assignmentId: "as_x7vfbq8owm"
costUsd: 1.6685216999999997
tokens: 83426
turns: 33
createdAt: "2026-11-15T21:57:00.741Z"
updatedAt: "2026-11-15T21:57:44.856Z"
---
## What I did
I read the code for the town's abstractions: ask, card, need, entry, thread, job, grant, gate, retainer, request, rule, reorg, fork and lane. I started from the examples Mitchell named. Then I searched core, runtime and server for `fallback`, silent `catch {}` blocks and `??` defaults in the code that writes cards and handles money. I changed no code. I proposed fix grant gr_eztubyh7nf and wrote topic page [dc_fu5unwj1kr](../../wiki/2026-11/2026-11-15-fallback-audit-decision-5-5unwj1kr.md).

## Findings
Mitchell's line refs have moved. createAsk's adopt/fold is now `packages/core/src/ask-verb.ts:64-71`. The queue's raw rows are at `packages/web/src/panels/queueOrder.ts:72-80`. The rollup Needs-to-asks conversion no longer exists, because rollups are refused. The other two cases are still in the code: propose_grant's "the town writes one", which now survives only as a stale description, and the facilitator fallback.

**Fail visibly (ranked by harm)**
| # | Where | What happens today | What a user sees | Recommendation |
|---|---|---|---|---|
| 1 | ask-verb.ts:64-71 + verbs/index.ts:26 | When a live ask already has a recommendation, a second card's body, recommendation and claims are dropped. Only a source line is appended. The adopt path keeps the old title over the new body. | The manager is told "your words are on it", which is false. The human decides from an older card, possibly one written by someone else. | Fail. Refuse, naming the open ask's id, or say truthfully what was kept. |
| 2 | secretary.ts:322-334 (via ask-verb.ts:112) | The ledger-rule ask is assembled by code: a template title "Add this rule to the ledger? …", the rule line as its body, an empty recommendation and no structure check (`refuse=false`). With no Secretary agent it is filed as `system` / `code`. | A policy card with no recommendation. That is the "ask written by code" Mitchell ruled out. | Fail. The Secretary's `rank pattern` gives its own title, body and recommendation. Refuse without them or without a Secretary. |
| 3 | schema/index.ts:2345, verbs/grants.ts:43 | The tool description says "Left out, the town writes one". In fact the code writes only a need. If a card is given and no need was filed, the card is silently dropped. The card's title is a code template (`proposalTitle`). | Agents believe a card exists when none does, and the proposal waits unrendered. | Fail. Fix the description, throw when a card has no need, and take the title from the author. |
| 4 | jobs.ts:362-366 → needs.ts:57-66 | `appendEntry` returns null both for a missing job and for an id it already wrote. Callers ignore the null: needForProposal (asks.ts:293), askForRetainer (:327), needForRequest (:342) and needAtTownHall. | A proposal or request with no need and no card. It shows only as a raw row in the human's queue. | Fail. Throw on a missing job and return the existing entry explicitly on a duplicate. |
| 5 | queueOrder.ts:72-80, DecisionQueue.tsx:283-288 | Items with no ask (reports, proposed or checkpoint grants, retainers, captain, access, goal proposals) are shown as raw rows that act like cards. | Buttons with no card, no recommendation and no claims. | Fail visibly but keep the row: label it "not rendered: <manager> hasn't written its card (en_…, N min)". Hiding the row would lose the item. |
| 6 | asks.ts:628 | A missing step-report verdict is printed as "Its verdict is continue" in the gate's facts. | A money card can tell the human that the forks said continue when they said nothing. | Fail. Write "it gave no verdict". |
| 7 | grants.ts:551, grant-forecast.ts:22,66, asks.ts:302,601-602, web asks.ts:112, StepStrip.tsx:45 | An unsized step (stored schema index.ts:1361 allows it; it only affects old grants) is priced and forecast as M. | Wrong ask, forecast and gate numbers for those grants. | Fail. Back-fill sizes or mark old steps unsized, make size required, and refuse to price an unsized step. |
| 8 | grants.ts:567-569 | At queue time, `catch { model = null }`: a step whose model the building no longer allows runs on the default model, and missing pages are dropped. | The funded plan says Fable but the fork runs on Opus, with a different cost and quality. Nobody is told. | Fail. Hold the step and write a thread entry naming the mismatch for the manager. |
| 9 | store.ts:175 (secrets back-fill) | A malformed MUSTER_TOWN_DATA_KEY throws in `dataKeyFrom`. The error is swallowed, so 0 keys are encrypted and nothing is logged. | API keys stay in plaintext, unnoticed. | Fail. Refuse to boot on a malformed key. |
| 10 | goal-changes.ts:116-120, meetings.ts:42-57 | When the Planner can't run, a reorg meeting is facilitated by the first manager, with no notice. With no manager, it falls back to the Planner even though the Planner can't run. `defaultFacilitator`'s last resort `attendees[0]` may be a stopped agent. | A reorg run by a different agent than promised, or a meeting that never moves. | Fail. Post a meeting notice naming who facilitates and why. Never pick an agent that can't run. |
| 11 | ask-checks.ts:151 | If the secret store errors, the code silently uses the host's env GH_TOKEN for claim checks. | Claim checks run with another credential. | Fail. Put the error in the check's note. |
| 12 | redeploy.ts:372,417 | If `isManage` or `inMeeting` throws, the code treats it as false. | A restart may cut a manage session or a live meeting. | Fail. Treat an error as busy and log it. |
| 13 | memory.ts:154, meetings.ts:393 | A topic-page search error gives [], and a deck error gives null. | A fork gets no topic pages, or a presentation shows nothing, and no one knows why. | Fail. Return the error in the prompt or meeting line. |

**Keep, with reason**
| # | Where | Why keep |
|---|---|---|
| 14 | bank.ts:57-64 (unknown model priced as Opus 5.5) | ops.ts:434 already posts a visible `unknown-model` event. Refusing to book would lose spend. |
| 15 | lanes.ts:71-80 (a continuation inherits its lane, otherwise the work is directed) | This is a documented rule, and agents in goal-directed buildings are refused at line 76. |
| 16 | runtime work.ts:103-150 + prompts.ts:800 (fallback report) | A dead session has to be recorded, and the report says the runtime wrote it. One small change: label the agent's last text "Last words", not "Findings". This assignment's own entry, en_se_j7g1yx4ymq ("The sweeps are still running"), read as progress. |
| 17 | runtime index.ts:389-397 (docker down → host backend) | Only in `auto` mode, and it logs a warning. I don't know prod's desk backend setting. If it is `auto`, this moves to fail. |
| 18 | main-fix.ts:41-47 (red-commit fix routed to this building) | It says so in the assignment text. |
| 19 | desk-bill.ts:70-72 (size cap fallback) | It is flagged on the handle and in the session (desk/session.ts:159). |
| 20 | asks.ts:327-333 (retainer need goes on the building thread when the retainer has none), asks.ts:616 ("The town" as recommender) | These are facts for the manager who writes the card. They are not the card itself. |

Not done: I didn't search packages/web beyond the queue. 158 `catch` blocks exist in core, runtime and server. I read the silent one-line ones, not all of them.

**Grant:** gr_eztubyh7nf (proposed, 300,000 tokens, 2 M steps). Step 1 fixes ranks 1-5, step 2 fixes ranks 6-10. Similar grants spent 241k–272k. Its need is waiting for Mara to render the card. Ranks 11-13 are small and can ride along in step 2 if there's room.

## What I need from you
Decide whether to fund gr_eztubyh7nf (Mara renders its card first).
