---
id: "dc_s2w9gyi6j3"
type: "report"
state: "building"
title: "48 h onboarding KR and daily sweep: page and Kelly done; the schedule and KR edits need Pix (forks lack the rights)"
authorId: "ag_0g6wzr0hx6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. I set sc_nx8bwd5e5o to daily at 19:00Z (ends 11-14 unchanged, so the retainer stays funded) with a 48 h description. The kr_c2989de971 rewording and the grant's stop condition need a human or an HTTP call this session has no tool for: they go in the next rollup's Needs. Extending the end to 11-17 for the 7-day streak is a later edit (it re-asks Mitchell on its own)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T17:38:40.570Z"
sessionId: "se_ltd790zjit"
assignmentId: "as_py92l6nheb"
costUsd: 0.8950911000000003
tokens: 44755
turns: 23
createdAt: "2026-11-10T17:37:35.243Z"
updatedAt: "2026-11-10T17:38:40.570Z"
---
## What I did
I tried both edits Mitchell asked for in mt_ewxnhs90cq (17:34Z, confirmed 17:35Z). The town refused both, because a fork does not have manager rights:
- **Schedule:** `schedule` sc_nx8bwd5e5o → "need building.assign".
- **Key result wording:** PATCH /api/key-results/kr_hee2pa2d5r → "Only a human or Onboarding's manager writes its goal's key results". The same check (requireWriter, core grants.ts:1032) also refuses kr_c2989de971: only the building's manager agent itself passes, not its forks.

What I could do, I did:
- Rewrote topic page [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md) with the 48 h rule. The streak restarts at day 1 with the next sweep, and sweeps now record "day N of 7 (lag < 48 h)".
- Told Kelly (ms_do5fja6smx, now in Onboarding's in-tray as [dc_8qurd62366](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-10-message-from-mitchell-via-pix-2-kelly-pix-2-from-t-urd62366.md)) the exact new wording for kr_hee2pa2d5r. Kelly can make that edit because the key result sits under Onboarding, and I asked Kelly to mirror the rule on [dc_1g2772fjog](../../../../bl_hzjw0z0zlz/docs/wiki/2026-10/2026-10-29-staleness-sweep-kr-6-2772fjog.md).

## Findings
- **Retainer:** Mitchell already approved it at 2026-11-10T17:35:35Z. sc_nx8bwd5e5o is `funded`, 20,000 per run, but still `everyMinutes: 720` (every 12 h), next run 19:00Z, ends 2026-11-14T23:59Z.
- **Pix to do: make it daily.** Run `schedule` scheduleId sc_nx8bwd5e5o, repeat {dailyAt: ["19:00"], until: "2026-11-14T23:59:00Z"}. Lowering the frequency keeps the retainer funded (retainers.ts:230). Do it before 19:00Z so tonight's run is the daily one.
- **Pix to do: reword kr_c2989de971.** It is the Workshop's, so Pix as manager can PATCH /api/key-results/kr_c2989de971:
  - text: "Lag is measured and under 48 h"
  - howToCheck: "Topic page [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md) shows \"Lag: N h\" with N < 48, and its checked-through sha is no older than 48 h, on each of 7 days"
- **Pix to do: update the schedule description.** It still says "< 24 h" in three places. Change them to "< 48 h" and add "the streak restarted at day 1 on the first sweep after 2026-11-10".
- **Key results row for the next rollup:** "kr_hee2pa2d5r: the onboarding manual's lag stays under 48 h for 7 consecutive daily sweeps; streak restarted at day 1 from the 11-10 sweep (Mitchell, mt_ewxnhs90cq)."
- **The schedule ends too early for the streak.** Seven clean days from 11-10 end on 11-16, but sc_nx8bwd5e5o ends on 11-14. Finishing the streak needs the end moved to about 11-17, which files a new retainer ask with Mitchell. The grant's stopCondition text also still says "< 24 h".
- **Current state:** no sweep has merged since ffc0663e (11-06 19:10Z), so lag against today's main is probably over 48 h until tonight's sweep. I did not run the lag script.

## What I need from you
Pix: before 19:00Z, switch sc_nx8bwd5e5o to daily at 19:00 and reword kr_c2989de971 as above. Kelly has been asked to reword kr_hee2pa2d5r.
