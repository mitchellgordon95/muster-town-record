---
id: "dc_brmyua9vvt"
type: "report"
state: "building"
title: "Exploration: no alert fires when live falls behind prod; proposed gr_h2iocyzfjm (200k)"
authorId: "ag_q9t71gnjff"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done; proposal gr_h2iocyzfjm filed and its ask written for Mitchell. Nothing to queue until he decides."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-17T03:28:48.184Z"
sessionId: "se_i6pt7ek8go"
assignmentId: "as_quqvc8s9mx"
costUsd: 0.7611744
tokens: 38059
turns: 15
createdAt: "2026-11-17T03:27:45.795Z"
updatedAt: "2026-11-17T03:28:48.184Z"
---
## What I did
Read live /api/health, origin/prod, monitor.ts, the pinger and ci.yml, under goal ob_648ua06ht0 (alert Mitchell before a human notices). Wrote findings [dc_cjihsuf48q](../../note/2026-11/2026-11-17-findings-no-alert-fires-when-the-live-server-falls-ihsuf48q.md) and proposed gr_h2iocyzfjm.

## Findings
- At 03:26Z on 11-17, live health was 5974c42b (started 18:52:32Z on 11-16). origin/prod was at 7a886f88 (02:11:46Z). So live had been behind for about 8.5 h, and `monitor.alerts` was empty. Mara noticed it ([dc_4yrb3979ty](../../../../town-hall/docs/fyi/2026-11/2026-11-16-nothing-merged-since-18-52z-is-live-ci-s-deploy-to-rb3979ty.md)), not the monitor. The same thing happened on 11-04 ([dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md)).
- None of the 11 monitor keys compares the live commit with prod.
- The pinger on Wright's box already forwards any red key by SMS and email, so a server-side key needs no change on his box.
- GitHub's branches API answers unauthenticated (200). Docs-only commits are skipped by CI on purpose (ci.yml lines 62-63), so the check must ignore them.
- Proposal gr_h2iocyzfjm, "Alert when the live server falls behind prod": a new `deploy` key polls GitHub every 5 min. It goes yellow at 30 min behind and red at 90 min. A GitHub error leaves it unknown, never red. Health also gets a `deploy` block. Two steps, M + S = 200,000 tokens. Key results: kr_tqbfyq8qlt, kr_k1isuqoxt5, kr_c4xz3cdyaz.

## What I need from you
Fund, counter or reject gr_h2iocyzfjm in the Town Hall in-tray.
