---
id: "dc_px0f53iitq"
type: "report"
state: "building"
title: "Cache alert: a false alarm. The check fires on the day's first session, and its 20% share test passes on every healthy day"
authorId: "ag_i8i09oipm8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Relayed to Mitchell in mt_4oj5dwfq25 with the doc attached; asked him whether the Workshop or Nell opens the cache-miss.ts fix (Bank Transparency's code). Folds into rollup 51."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-06T04:05:05.856Z"
sessionId: "se_4m3yqq9fgn"
assignmentId: "as_tcsgd0sdm3"
costUsd: 1.0952226
tokens: 54761
turns: 24
createdAt: "2026-11-06T04:04:48.682Z"
updatedAt: "2026-11-06T04:05:05.856Z"
---
## What I did
I paged 40k events (11-01 to 11-06 04:02Z) from `/api/events?since=`, pulled every `alert: cache-miss`, and re-ran core `cacheMissCheck` over the full days 11-04, 11-05 and 11-06. I also counted 5-minute against 1-hour cache writes per day. I tried to read the transcripts for first-turn numbers and got 403: forks can't read them, even for Workshop sessions. I couldn't speak in the 1:1 (only Pix can), so Pix needs to pass this on to Mitchell. No PR, no redeploy. Page: [dc_rmujej9qgt](../../wiki/2026-11/2026-11-06-cache-miss-alert-hud-cache-alert-ujej9qgt.md).

## Findings
**Today's events, verbatim** (ids 135616 and 135623, at 00:00:30Z and 00:00:40Z):
- "Cache miss: work sessions on claude-opus-5-5: 1 h cache writes were 72% of today's cost (alert above 20%); 1 session: se_ka444n4m47". Reasons ["share"], firstTurn [], usd 0.28.
- "Cache miss: manage sessions on claude-fable-5-1: 1 h cache writes were 79% of today's cost (alert above 20%); 1 session: se_whuzgpvdkg". Reasons ["share"], firstTurn [], usd 0.36.

**The sessions:**
- se_ka444n4m47: Teo 1, a UI/UX work fork on Opus, 5 turns, cacheRead 263,891, cacheWrite1h 25,418.
- se_whuzgpvdkg: Teo's manager wake on Fable, 5 turns, cacheRead 98,309, cacheWrite1h 14,189.

Neither tripped the first-turn test, so each first turn read at least as much as it wrote. Neither is a Workshop fork started after acda269. Nothing is wrong with the prompt layout.

**Why it fires anyway: two flaws in core `cache-miss.ts`.**
1. **It judges a purpose on the first session after midnight, then goes silent for the day.** 11-05 shows the same pattern: three alerts at 00:00–00:02Z, each on 1 session (se_bmmk1dum2f, se_fmdh4l7ozz, se_bqewuchmw0). After that, no later session of those purposes gets checked that day.
2. **The 20% share test can't tell a broken layout from a healthy one.** Since 11-04 every cache write is billed at the 1-hour rate:

   | Days | Sessions with any 5-minute write |
   |---|---|
   | 11-02 | 83 of 174 |
   | 11-03 | 75 of 166 |
   | 11-04 to 11-06 | 0 of 787 (the last was se_5jf9det0fc, 11-03 23:37Z) |

   So ordinary turn-by-turn writes now count toward the share. Over whole days, the share is the same with the layout broken and fixed:

   | Day | Layout | work/Opus | manage/Fable |
   |---|---|---|---|
   | 11-04 | broken | 44% | 66% |
   | 11-05 | fixed | 46% | 66% |

   Both are far above 20%, so the share test will fire every day.

The first-turn test is the one that did its job: on 11-04 it named 9 work forks writing about 50k with 0 read, and 8 manager wakes writing 31–39k with 0 read.

I couldn't confirm which change made every write a 1-hour write. It isn't in this repo's runtime code; it is probably the CLI/SDK's cache TTL default.

**The fix (one line's worth):** in `cacheMissCheck`, drop the "share" reason, or gate it at ≥10 sessions in the group with a threshold above about 70%, and keep only the first-turn reason. Ideally, also evaluate after the day's sessions rather than locking each purpose on its first one. This is Bank Transparency's code (gr_lwgus14rd2, kr_f49co6lg51), so by the merge rules Mitchell has to OK it first.

## What I need from you
Tell Mitchell in the 1:1 (mt_4oj5dwfq25) that the alert is a false alarm and nothing regressed, and ask whether the Workshop should open the cache-miss.ts fix or pass it to Nell (Bank Transparency).
