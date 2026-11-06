---
id: "dc_7wrr65srdo"
type: "report"
state: "building"
title: "Cache-miss alert redefined around prefix busting (PR #364, parked on CI): a session busts when most of its turns 2+ re-write ≥ 50% of their prefix; the alert fires per purpose above 10% busting sessions, naming the worst"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #364 open; the directed continuation is replaced by a grant-lane assignment (the grant is funded again at 850k)."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-05T20:01:16.772Z"
sessionId: "se_191wluaxtp"
assignmentId: "as_es824n3ryo"
costUsd: 3.7168889500000004
tokens: 185844
turns: 26
createdAt: "2026-11-05T19:59:59.598Z"
updatedAt: "2026-11-05T20:01:16.772Z"
---
## What I did
Mitchell's decision 3 in 1:1 mt_pr3347g2w2: the cache-miss alert (gr_lwgus14rd2 step 2, kr_f49co6lg51) should catch a session whose context changes every turn, busting the cached prefix, not the 1 h cache-write share of cost. I rewrote core `cache-miss.ts` and its runtime hook, measured a live baseline first, updated the tests, docs/prompt-caching.md and docs/log.md, and opened draft PR #364 (commit 3947ec76): https://github.com/mitchellgordon95/muster-town/pull/364. Typecheck, docs check and the three affected test files pass (51 tests); the fast check passed everything but one web test I then fixed (the Spending table no longer tints the cache-write share red over 20%). Full CI (knip included) runs on the PR; I park on it.

## Findings
- **The measure.** Per session, from its stored transcript, one turn per `message.id` (a call's blocks repeat its usage). For turns 2+, re-write rate = cache_creation / (cache_read + cache_creation). A turn busts at ≥ 50% (`BUST_TURN_RATE`); a session busts when more than half of at least 2 such turns bust, so a single compaction turn is not a bust. Turn 1 never counts (cold start). Per purpose, the alert fires when busting sessions pass 10% (`CACHE_MISS_SHARE`) of the day's ended sessions with a signal; sessions without a transcript or with fewer than 2 turns after the first are counted as `noSignal`. One `system` event `alert: cache-miss` per purpose per day, naming up to 10 worst sessions (highest share of busting turns, then most tokens re-written) with turns / bustTurns / rewritten; the HUD line works unchanged.
- **Live baseline** (37 Bank Transparency sessions of 11-04/05, read through GET /api/sessions/:id/transcript with the manager token): turns 2+ re-write 1–14% of their prefix (median per session), max 20% on any turn; no session busts. So 50% per turn leaves a clear margin over healthy sessions, and the alert is quiet on a healthy day. I could only read my own building's transcripts; other purposes (manage of other buildings, 1:1s) are unmeasured but the same layout applies.
- **Dropped:** the 1 h cache-write share threshold (the 20% question in [dc_dxz4r8vifo](2026-11-04-checkpoint-gr-lwgus14rd2-lane-token-kind-table-liv-z4r8vifo.md)) and the first-turn rule (always true on a cold start). The share stays as the Spending lane × kind table's "Cache-write share" and "Write 1 h" columns, now without the red tint at 20%.
- The grant's KR text for kr_f49co6lg51 still describes the old 20% rule; the grant stays at checkpoint (top-up 250k pending). Held as_wd0gpawhhk (verify the old alert live) should be re-worded to verify this one once #364 is live; I'll do that when I resume.

## What I need from you
Nothing needed.
