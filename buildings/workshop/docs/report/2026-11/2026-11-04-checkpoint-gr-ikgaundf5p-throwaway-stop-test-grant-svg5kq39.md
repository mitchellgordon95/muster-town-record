---
id: "dc_4esvg5kq39"
type: "report"
state: "building"
title: "Checkpoint gr_ikgaundf5p (throwaway stop-test grant): nothing to ship by design; press Stop grant… on this card to run gr_8i952perny's live check"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_8uptthmx6m"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Secretary\": Cluster the daily digest card's \"Shipped since last digest\" by theme instead of a flat list (Mitchell, 1:1 mt_i50xwu4z2t: \"the digest is still overwhelming, can"
decidedBy: "ag_7tiwyqva83"
decidedAt: "2026-11-04T18:04:29.071Z"
sessionId: "se_uy9yikaicn"
assignmentId: "as_qqwaum4lbj"
costUsd: 1.7028720999999998
tokens: 85144
turns: 13
createdAt: "2026-11-04T18:03:36.249Z"
updatedAt: "2026-11-04T18:04:29.071Z"
---
Live edb3201 (GET /api/health read at 18:02:12Z 11-04). This is the checkpoint for the throwaway grant you funded 12 minutes before it; no code shipped on it, by design. Wiki page dc_a1xvdmr2xe holds the state.

## Shipped
**1. The throwaway grant is funded and held at its checkpoint, ready to be stopped**
**What it is:** gr_ikgaundf5p exists only so you can press "Stop grant…" on a real funded grant and the Workshop can read the Bank and the in-tray before and after (the live half of gr_8i952perny's key results kr_kaz3nj127k and kr_f46tddd9as). Nothing was assigned on it. It crossed 100% at once because the town's own kickoff session (59,440 tokens on Fable) is charged to the grant and cost more than the 5,000 you funded; that is the paperwork-cost problem proposal gr_k69g04wwcg addresses. API-only: the grant's state is GET /api/grants/gr_ikgaundf5p (status checkpoint, spent 59,440 of 5,000, fund 17:50:38Z, checkpoint 18:01:33Z).
**What you'd see:** Town Hall in-tray: this checkpoint card with "Stop grant…" on it (it shows on checkpoint grants as well as funded ones). Bank page free tokens before any stop: 7,624,538 (GET /api/bank at 18:02:12Z). Because spent exceeds granted, the unspent rest is 0 and free tokens will not rise on the stop; the "Stopped: for the record" row with your reason, this key result missed with "Grant stopped: <reason>", and the history close line will still appear.
**Your call:** Press Stop grant… on this card with any reason. If you also want to see the Bank's free tokens rise, Adjust it to 150,000 first, then Stop: the unspent rest (about 50,000) returns.

## Decided
- [dc_8uptthmx6m](2026-11-04-gr-ikgaundf5p-throwaway-stop-test-grant-funded-not-ptthmx6m.md) → approve (my own kickoff report: nothing assigned, fallback close sc_060f0dnpd2 on 11-06 12:00Z, held while the grant is at checkpoint)

## Key results
| Grant | Key result | Status | How to check | What the check showed | Spent / granted |
|---|---|---|---|---|---|
| gr_ikgaundf5p | kr_una0o5bucs Mitchell stops it from the in-tray; free tokens rise by the unspent rest; "Stopped: for the record" row (due 11-05) | not-started | Bank free tokens before/after (GET /api/bank); in-tray stopped row with the reason; GET /api/grants shows the KR missed with "Grant stopped: <reason>" | Not stopped yet. Before: free tokens 7,624,538 at 18:02:12Z; unspent rest will be 0 (spent 59,440 > 5,000) so free tokens stay flat; the row, the missed KR and the history line are still testable | 59,440 / 5,000 |

Spend today by lane: exploration 72,681 tokens (free under the Workshop goal 7,624,538); directed 269,611 tokens.

## Needs from Mitchell
Stop gr_ikgaundf5p from this card (Stop grant… with any reason) rather than Continue or Cut: the stop is the test. Cut also ends it but does not exercise the stop path.

_Already waiting in your in-tray: 1 proposal (gr_k69g04wwcg), 1 request ([dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md)), 3 rollups ([dc_yrfnb5ebyc](2026-11-04-workshop-rollup-43-the-in-tray-is-a-one-line-list-fnb5ebyc.md), [dc_m243f169x2](2026-11-04-workshop-rollup-44-closing-a-grant-as-done-now-mar-43f169x2.md), [dc_hp4k1pg9qu](2026-11-04-workshop-rollup-45-the-secretary-is-in-the-town-ha-4k1pg9qu.md))._
