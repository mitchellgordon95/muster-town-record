---
id: "dc_gj47hpjxu8"
type: "report"
state: "building"
title: "1:1 lines show their tool calls, folded (PR #423 draft, parked on CI)"
authorId: "ag_dy21ge2g82"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: draft PR #423 (1:1 lines carry their tool calls, folded; no migration, no new polling) is parked on CI as as_4h4fmxc0zt, which merges it when green and checks it live. Nothing else to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-10T21:10:06.884Z"
sessionId: "se_rwzc09ipy2"
assignmentId: "as_4s92hc3iqx"
costUsd: 2.0854909000000004
tokens: 104275
turns: 50
createdAt: "2026-11-10T21:09:58.081Z"
updatedAt: "2026-11-10T21:10:06.884Z"
---
## What I did
Built Mitchell's request from 1:1 mt_db6itzy2br: tool calls, summarized, in 1:1s and other meetings. Server, client and mock are done, with a test. Draft PR #423 (https://github.com/mitchellgordon95/muster-town/pull/423, commit 37425715). Topic page [dc_7hxvocdq31](../../wiki/2026-11/2026-11-10-tool-calls-in-1-1s-and-meetings-xvocdq31.md).

## Findings
- **The record stays on the server.** When an agent speaks, `meetingSpeak` stores the `agent.tool` events it made since its previous line in that meeting. They go on the utterance as `tools`, with at most 30 calls and its own listen/speak calls left out. It is an optional schema field, so no migration. The transcript still shows the calls after the meeting ends.
- **No raw input is ever shown.** Each call is the describeTool one-liner. A result line, from the in-memory toolResults ring, is kept only for town tools and for errors. Errors show in red. Token-like strings become [hidden]. Lines spoken after a restart have no results, because the ring is empty then.
- **The live line costs nothing new.** Under "Moss is writing…", the panel shows "▸ Moss: N tool calls so far", built from the events feed the client already has. It adds no polling. Live lines have no results; the posted line carries them.
- **What a human sees for 5 reads and a grep** (checked in the mock town in Chromium at 1280×800): a muted, folded "▸ 6 tool calls" between the name and the reply. Opened, it shows one line per call, e.g. `Reading "Bank fees: what a donor pays" → # Bank fees…`, with the failed grep in red. Screenshots: /api/media/mf_17ysh0ymkt.png (live) and /api/media/mf_l4syz6r0lx.png (posted).
- `npm run check --fast` is green: typecheck, docs, and 58 web test files with 309 tests, plus the new core test meeting-tools.test.ts. Not yet seen on live.

## What I need from you
Nothing needed. Next session: merge #423 once CI is green, then check it on live.
