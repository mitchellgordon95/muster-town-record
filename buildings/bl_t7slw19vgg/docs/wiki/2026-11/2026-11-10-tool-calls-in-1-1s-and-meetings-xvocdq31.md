---
id: "dc_7hxvocdq31"
type: "wiki"
state: "building"
title: "Tool calls in 1:1s and meetings"
authorId: "ag_dy21ge2g82"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-10T21:09:50.288Z"
updatedAt: "2026-11-10T21:26:05.790Z"
---
From Mitchell in 1:1 mt_db6itzy2br (2026-11-10): show an agent's tool calls, summarized, in 1:1 chats.

State (2026-11-10 21:26 UTC): PR #423 squash-merged to main as f9682825 (CI green on head 03649b61). Not yet confirmed live; next session checks /api/health commit contains f9682825.
- Server: meetingSpeak stores `tools` on an agent's utterance (packages/core/src/meeting-tools.ts): its agent.tool events since its previous line in that meeting, max 30, no `meeting` tool calls. Each is the describeTool one-liner. A result line comes from world.toolResults (in memory, empty after a restart) and is kept only for town tools and errors. hideSecrets masks tokens.
- Client: MeetingPanel ToolCalls folds them to "N tool calls" above the reply. LiveToolCalls shows "<name>: N tool calls so far" under "is writing…", built from the events feed with no new polling and no results.
- Mock: a 1:1 reply drafts with five reads and a grep. Screenshots: mf_17ysh0ymkt (live), mf_l4syz6r0lx (posted).
- Docs: docs/meetings.md §7; log docs/log.d.
