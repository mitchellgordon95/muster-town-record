---
id: "dc_xnofgjydsw"
type: "report"
state: "building"
title: "Uptime block no-key wording: PR #475 open, parked on CI"
authorId: "ag_e1fn1kxw0d"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on PR #475 CI; continuation as_slyixjbj1x is queued (waiting {pr:475}) and merges on green without a redeploy. Nothing else needed."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-16T18:24:47.798Z"
sessionId: "se_zf8uqrgp57"
assignmentId: "as_us2v12hqm7"
costUsd: 0.5845146
tokens: 29226
turns: 13
createdAt: "2026-11-16T18:24:39.324Z"
updatedAt: "2026-11-16T18:24:47.798Z"
---
## What I did
Made the Uptime block honest when no UPTIMEROBOT_API_KEY is set, rewrote docs/self-host.md item 10 and fixed the stale line in docs/architecture.md. Commit 1be7a109, draft PR #475 (https://github.com/mitchellgordon95/muster-town/pull/475). `npm run check --fast` passed: docs, deadcode, typecheck and tests (60/60 web, including uptime.test.tsx 4/4). The work is parked until CI finishes.

## Findings
- packages/web/src/panels/Uptime.tsx now takes the server's `error` field from /api/uptime. Three cases:
  - **No key** (error starts "no UPTIMEROBOT_API_KEY"): the block says "Not measured. · No uptime monitor is set up for this town: set the UPTIMEROBOT_API_KEY secret to show uptime". It no longer says "Measured by UptimeRobot". The grey strip and the restart list still show.
  - **Key set but the read failed**: "Not measured right now. · Measured by UptimeRobot; it gave no number (<reason>)".
  - **Key set but the monitor is too new to have data** (error null): "Not measured yet", as before.
- The test file adds both new cases. BankPanel and home/main.tsx use UptimeView/UptimeBlock unchanged. The typecheck passed.
- docs/self-host.md item 10 is marked fixed. It says what a self-hoster sees before and after setting the key, and what UPTIME_STATUS_URL adds.
- docs/architecture.md:234 now says the server reads getMonitors with the key, and that `pct` is null with `error` set when there is no key or the read fails. I changed nothing else that mentions town.uptime.
- The log entry is docs/log.d/2026-11-16-cleo-1-uptime-no-key-wording.md.
- Not covered: the static placeholders (`home.ts:120`, `home/main.tsx:47` fallback) still say "Measured by UptimeRobot: /api/uptime". They show only before the figures load, or if they fail to load. I left them as they are.
- No live check is needed. muster.town has the key set, so only the null-pct branch changes.

## What I need from you
Nothing needed. On resume: if CI is green, mark #475 ready and merge it (no redeploy), then report with the merge sha and verdict stop.
