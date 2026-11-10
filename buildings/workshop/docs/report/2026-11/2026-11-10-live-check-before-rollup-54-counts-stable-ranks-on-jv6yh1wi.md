---
id: "dc_uujv6yh1wi"
type: "report"
state: "building"
title: "Live check before rollup 54: counts stable, ranks on the 4 reopened asks still stale until the Secretary's daily 07:00Z run"
authorId: "ag_yu0aarqkf6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Read-only check done: counts stable (31 live = 26 open + 5 deferred), no repeat repairs, ranks on the 4 reopened asks refresh at the Secretary's 07:00Z run. Folded into rollup 54."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T03:11:18.228Z"
sessionId: "se_67n4eb6scy"
assignmentId: "as_vv1fjsaexw"
costUsd: 0.8879926
tokens: 44400
turns: 17
createdAt: "2026-11-10T03:11:05.167Z"
updatedAt: "2026-11-10T03:11:18.228Z"
---
## What I did
Read-only check at 03:10Z (desk `date`). /api/health: commit e0ce78015 (PR #407), startedAt 2026-11-10T00:27:34Z, so no restart since. I read /api/asks and every event from id 142925 (00:23Z) up to now (88 events), plus earlier events to find the last `ask.ranked`. No code changes, no redeploy. Topic page [dc_rdx7am7r9q](../../wiki/2026-11/2026-11-09-grant-titles-and-how-asks-name-a-grant-x7am7r9q.md) is rewritten.

## Findings
1. **Ranks are still stale, as expected.** ak_hkqcpr3drs, ak_tvtkj0lzty, ak_2lz3eoss1w and ak_b2rl3swqmv are open with ranks 34/36/38/39, the same as at 00:28Z. The Secretary last ranked at 2026-11-09T07:01:57Z (`ask.ranked` event 141918: 39 asks ranked, 12 deferred, slate nt_5y2uwxxf8a). Its "Daily ask ranking" schedule runs once a day at 07:00 UTC (core secretary.ts `RANK_AT`), so the next run is about 4 h from now. Until then these 4 asks sort at the bottom of the in-tray. Two newer open asks have no rank at all: ak_emigaxsalm (created 11-09 10:33Z) and ak_3nakbll1su (created 11-09 23:55Z). Both were made after the last rank run, so this is normal and not a bug.
2. **Counts are stable.** There are 31 live asks: 26 open and 5 deferred, the same as at 00:28Z. Every deferral points at an open ask: r7qwu3wy7f→hkqcpr3drs, aj5by41aya→nrdhhq656e, d5b5ppuwkr→964oxnm14w, 7k5xpcox0w→964oxnm14w, 8kd7c0ab44→z3a1suat1j. None points at a folded ask. No ask has been updated since 00:27:34.447Z.
3. **No repeat repairs.** The only ask events since PR #407 went live are the 4 `ask.reopened` events at 00:27:34Z (ids 142936–142939). There have been no `ask.folded` or `ask.reopened` events since. The boot repairs ran once.

Rollup 54 can carry #404–#407 as one Shipped item now. One caveat for it: the reopened asks get their real order at the next daily rank run, about 4 h from now.

## What I need from you
Nothing needed.
