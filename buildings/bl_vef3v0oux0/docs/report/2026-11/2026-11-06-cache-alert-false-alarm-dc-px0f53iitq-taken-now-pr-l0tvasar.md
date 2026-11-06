---
id: "dc_pcl0tvasar"
type: "report"
state: "building"
title: "Cache alert false alarm (dc_px0f53iitq): taken now. PR #364 (prefix busting, already drops the share test) merged with main, gains a 5-session floor per purpose, ready and in CI on 98528e5b; parked to squash-merge when green"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_px0f53iitq","dc_wcfoeo59bn","dc_qnpvanlfsb"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/364"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #364 (98528e5b) ready with the 5-session floor; its continuation as_fim0vp3kmq resumed by itself when CI finished and squash-merges if green (no redeploy), then parks on the deploy. Pix's correction (ms_4ck3aagidx) confirms the rewrite is ours under gr_lwgus14rd2; the directed lane carried it because the grant is held at its checkpoint."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-06T04:11:41.851Z"
sessionId: "se_epkjtcyd95"
assignmentId: "as_ajgocy7dhe"
costUsd: 3.5821105999999996
tokens: 179106
turns: 29
createdAt: "2026-11-06T04:10:51.856Z"
updatedAt: "2026-11-06T04:11:41.851Z"
---
## What I did
Mitchell, via Pix (1:1 mt_4oj5dwfq25), passed on Pix 1's finding that today's HUD "Cache alert" is a false alarm from my cache-miss check. I took the fix now instead of waiting on who opens the PR, since it was already built: PR #364 (Mitchell's own redefinition of the alert from 1:1 mt_pr3347g2w2, prefix busting) was green but held because gr_lwgus14rd2 is at its checkpoint. I merged main into it (only docs/log.md conflicted; both lines kept), added the gate Pix 1 asked for, ran typecheck and the core, runtime and web finance tests (53 green), pushed, marked the PR ready, replied to Pix with the TTL answer from [dc_wcfoeo59bn](../../wiki/2026-11/2026-11-04-cache-ttl-why-every-cache-write-is-1-h-since-2026-foeo59bn.md), and rewrote the plan page [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md).

## Findings
- **Both flaws Pix 1 found are real and #364 already removes their cause.** The live check (38c3e992) judges each purpose at 00:00Z on the day's first ended session, and its 20% 1-hour cache-write share fires on every healthy day now that every cache write is billed at the 1 h rate (0 of 787 sessions since 11-04 had a 5-minute write; the TTL flip is explained in [dc_wcfoeo59bn](../../wiki/2026-11/2026-11-04-cache-ttl-why-every-cache-write-is-1-h-since-2026-foeo59bn.md): Claude Code's remote flag, not our code). #364 drops the share and first-turn reasons and judges each session on its turns 2+ (a turn busts at ≥ 50% of its prefix written fresh; a session busts when most of ≥ 2 such turns do; a purpose alerts above 10% busting sessions).
- **New in this session: `MIN_SESSIONS` = 5** in core `cache-miss.ts`. A purpose needs at least 5 ended sessions with a signal (a transcript with ≥ 2 turns after the first) before its busting share is judged, so the day's first session is never a verdict. 1 of 5 (20%) fires, 1 of 4 stays quiet, 1 of 10 (10%) stays quiet. Tests cover the gate in the pure check, the world check and the runtime tick. Documented in docs/prompt-caching.md.
- **Still one alert per purpose per day** after it fires (the events log is the memory), as designed; the fix is that it no longer fires on a healthy day.
- PR #364: https://github.com/mitchellgordon95/muster-town/pull/364, head 98528e5b, ready for review, CI check in progress at 04:10Z. On resume: squash-merge if green, no redeploy (CI deploys it), then park on the deploy to confirm the alert stays quiet live. The HUD's 300-event window flaw (an alert can scroll out of the client's view) is not in this PR; it stays in the held follow-up as_ail5blil47.
- PR #362 (manager wakes, step 3) stays held at the checkpoint: it is not part of what Mitchell asked about.

## What I need from you
Nothing needed.
