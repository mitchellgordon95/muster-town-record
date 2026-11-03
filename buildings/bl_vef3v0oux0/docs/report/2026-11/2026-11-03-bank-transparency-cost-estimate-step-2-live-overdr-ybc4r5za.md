---
id: "dc_quybc4r5za"
type: "report"
state: "building"
title: "Bank Transparency: cost estimate step 2 live, overdraft cause fixed at 85498fa, grant proposed for the new cache-monitoring goal"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_o1bx272hbw","dc_9973c6uh8x","dc_bot1ogt5dl"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_150clgy3am"
createdAt: "2026-11-03T02:47:02.366Z"
updatedAt: "2026-11-03T02:47:02.366Z"
---
Live: 85498fa (since 2026-11-02 20:41 UTC); a redeploy was waiting on this session.

## Shipped

**1. Grant proposals show a model-estimated cost range (PR #267, step 2 of the cost estimate)**
**What it is:** When a grant is proposed, one small model session reads the plan and similar closed grants and writes a cost range next to the ask; funded grants keep the history range only (estimate.ts:35/:61). Reports [dc_o1bx272hbw](2026-11-02-pr-267-grant-cost-estimate-step-2-merged-as-70d90b-bx272hbw.md), [dc_9973c6uh8x](2026-11-02-cost-estimate-step-2-is-live-at-70d90b7d-check-fin-73c6uh8x.md); check:finance 32/32 green at 70d90b7d.
**What you'd see:** Town Hall in-tray → a proposal card: "ask N · estimate …". Today's first live case is gr_lwgus14rd2: "ask 600,000 · 3 similar grants spent 289,904–698,207 (median spent/funded 0.91 across 31 closed grants; this building 0.95 across 8)". The Bank's FREE line now shows an overdraft as a red negative number:
![Bank FREE line negative, in red](/api/media/mf_k0u118kz0e.png)
**Your call:** None.

**2. The overdraft's cause is fixed and the "see it next time" goal has a plan (85498fa, Mitchell's Claude Code session here)**
**What it is:** Manager wakes re-wrote a 32K prefix to the cache every time (clock on line 2, wiki in the prefix): ~45K adj. tokens per Fable wake, 73% of 14-day spend was manager + directed sessions, ungated. 85498fa makes the manager prompt byte-stable (~13K per wake expected), gates directed work on free tokens and keeps the reserve for managers. Report [dc_bot1ogt5dl](2026-11-02-overdraft-of-2026-11-02-cause-found-prompt-caching-t1ogt5dl.md) (approved); new goal gl_vjek98yym0 with brief [dc_g7q7s2vug8](../../note/2026-11/2026-11-02-brief-token-cost-is-legible-and-watched-cache-moni-q7s2vug8.md). I proposed gr_lwgus14rd2 (600,000) against it: lane × token-kind table on Spending with cache-write share, a daily `alert: cache-miss` HUD event, manager wakes per building per day. Also queued one small exploration (as_ricjwkoaxc) to verify the fix on the first live wakes (turn-1 cache write before/after).
**What you'd see:** API/docs only so far (docs/prompt-caching.md). Once the exploration reports: the per-wake numbers in the next rollup.
**Your call:** The proposal is in your in-tray; nothing else.

## Decided
- [dc_o1bx272hbw](2026-11-02-pr-267-grant-cost-estimate-step-2-merged-as-70d90b-bx272hbw.md) → approve (PR #267 merged 70d90b7d, redeploy queued)
- [dc_9973c6uh8x](2026-11-02-cost-estimate-step-2-is-live-at-70d90b7d-check-fin-73c6uh8x.md) → approve (step 2 verified live; no open proposal then, so no model range to show)
- [dc_bot1ogt5dl](2026-11-02-overdraft-of-2026-11-02-cause-found-prompt-caching-t1ogt5dl.md) → approve (cause fixed at 85498fa; follow-up = proposal gr_lwgus14rd2 + exploration as_ricjwkoaxc)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_dt1l35tydx Spending tab says what each grant bought | kr_d3mh9gmk2k | not-started (step 2 as_8mbeonpgic pending, was held overdrafted) | 283,366 / 500,000 |
| gr_dt1l35tydx | kr_f5gx4nuzuu | not-started | 283,366 / 500,000 |
| gr_4tf9hd64d5 Grant pages list their sessions | kr_tqjylvupko | not-started (step 1 as_76vjraki6o held overdrafted) | 0 / 200,000 |
| gr_4tf9hd64d5 | kr_o550w4u25b | not-started | 0 / 200,000 |

Spend today by lane: exploration 0 tokens (free under our goal 1,291,011 at session start), directed 0 tokens. Queued this session: as_ricjwkoaxc (exploration, ≤40K).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_lwgus14rd2), 0 requests, 1 rollup ([dc_4s6sdf5p6g](2026-11-02-bank-transparency-spending-tab-per-grant-lines-neg-6sdf5p6g.md))._
