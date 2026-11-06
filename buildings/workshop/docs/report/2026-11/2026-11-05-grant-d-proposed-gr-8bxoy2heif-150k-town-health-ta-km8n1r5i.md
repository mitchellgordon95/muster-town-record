---
id: "dc_2dkm8n1r5i"
type: "report"
state: "building"
title: "Grant D proposed: gr_8bxoy2heif (150k), Town health tab + digest Health line; all metrics computable; Nell not yet answered"
authorId: "ag_siwx3cf0pp"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Grant D proposed as asked in the 1:1 mt_o0exccdv8g (gr_8bxoy2heif, 150k, no retainer). It waits on Mitchell in the Town Hall in-tray. If Nell answers that a hit ratio is queued in Bank Transparency, the funded work reads her endpoint."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T20:48:57.788Z"
sessionId: "se_h3c7bp9hue"
assignmentId: "as_jfu49apmz7"
costUsd: 0.8645971999999997
tokens: 43230
turns: 23
createdAt: "2026-11-05T20:48:28.940Z"
updatedAt: "2026-11-05T20:48:57.788Z"
---
## What I did
- Read engagement.ts, StatsPanel.tsx, secretary.ts (digest builder), the Session schema, grants.ts (holds), and Bank Transparency's cache code (cache-miss.ts, finance-lane-kind.ts).
- Asked Nell (ms_htdtsgucnz).
- Proposed **gr_8bxoy2heif** (150k, goal gl_join). It has 3 key results: the tab (kr_yz4mmbjqcv, due 11-09), the digest Health line (kr_4jctfoqcxt, due 11-10) and tests (kr_q30lbsiwxt).
- No code written. The plan is on topic page [dc_2ca8uygy5k](../../wiki/2026-11/2026-11-05-town-health-tab-grant-d-gr-8bxoy2heif-a8uygy5k.md).

## Findings
**Each metric can be computed from data we already store:**
- **Paperwork share:** sessions → assignments.title gives us kickoff sessions ("Grant … funded: assign its first step") and checkpoint sessions ("Write the checkpoint for …"). Manager wakes are the sessions with purpose `manage`/`review`. The share is that paperwork divided by (grant-lane spend + those wakes). The baseline was 26.7% ([dc_hqozax72qw](2026-11-04-grant-bookkeeping-re-cut-after-the-cache-fix-the-f-ozax72qw.md)).
- **Cache hit ratio:** cacheRead ÷ (cacheRead + cacheWrite5m + cacheWrite1h). These are raw counters on every session. Back-filled sessions are left out.
- **Cache write per session:** we can compute the median from the same counters. A true *first-turn* cold write needs the stored transcripts (cache-miss.ts `storedFirstTurn`), and not every session has one. So the tab shows the median cache write per session instead. The baseline was 58,714 raw tokens per kickoff/checkpoint session.
- **Overrun:** the `grant.checkpoint` event carries {grantId, fraction, spentTokens, grantTokens} and a timestamp. Overrun is the tokens of that grant's sessions that started after its 100% hold and before the next continue/adjust/cut. The baseline was 1,083,858 since the cache fix.
- **Tokens per report by lane:** sessions.reportId + lane.
- The digest's "Decisions needed" is built in code (secretary.ts `digestBody`/`digestCard`). So a "Health:" line built the same way costs no Secretary tokens. No retainer is proposed.

**Overlap with Bank Transparency's gr_lwgus14rd2 (from the code, status checkpoint):**
- It already serves the cost share of cache writes by lane × token kind on `/api/finance/spend`, plus a daily `alert: cache-miss`.
- No hit ratio, paperwork or overrun metric exists anywhere in the repo.
- The proposal reuses its helpers (laneKindRow, sessionTokens, isBackfilled) and links to Bank → Spending rather than pricing anything anew.

**Nell's answer:** none yet when I filed. The proposal says that if a hit ratio is queued in Bank Transparency, the tab will read her endpoint.

## What I need from you
Fund, counter or reject gr_8bxoy2heif in the Town Hall in-tray.
