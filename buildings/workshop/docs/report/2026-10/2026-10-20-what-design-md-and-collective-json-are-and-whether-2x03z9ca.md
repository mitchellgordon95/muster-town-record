---
id: "dc_ku2x03z9ca"
type: "report"
state: "building"
title: "What design.md and collective.json are, and whether they're still used"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "update the out of date stuff sure. if there's nothing wrong with the collective.json files, leave them alone"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:52:33.052Z"
sessionId: "se_wh1shuorrc"
assignmentId: "as_7dv8ytbrgv"
costUsd: 0.13402999999999998
tokens: 4496
turns: 7
createdAt: "2026-10-20T03:46:19.885Z"
updatedAt: "2026-10-20T03:52:33.052Z"
---
## What I did
Checked where the repo references and reads each file. I made no edits. This also answers your "what is this even talking about" on my PR #20 report: that report was about these two files.

## Findings
**docs/design.md**: the notes on what the town is for: your original asks, then each design review written down as it happened (reviews 1–4, the last dated 2026-10-20). No code reads it. Agents do: CLAUDE.md, AGENTS.md, the README and the workshop's job description all tell residents to read it first.
**Still used?** Yes, as reading material for agents. But the "Core concepts" table near the top still describes v0 (runs, desks listed in building.json). Newer sections below it overrule that, so an agent that only skims the top gets the old model.

**collectives/<name>/collective.json** (one each for climate and workshop): the setup file for one town instance. It holds the name, goal, port, moderators, and the buildings to create with their residents, reviewer, code workspace and budget. The server reads the port and name on every start (`packages/server/src/main.ts:21`). The buildings and residents are only created once, on the first start with an empty database (`packages/core/src/seed.ts:116`).
**Still used?** Yes, but after that first start, editing the buildings or residents in it changes nothing in the running town. You change those in the UI or database instead.

## What I need from you
Decide whether to (a) leave both files as they are, (b) let me update design.md's out-of-date "Core concepts" table, or (c) something else for collective.json.

## Reply from Mitchell (2026-10-19 23:52)

update the out of date stuff sure. if there's nothing wrong with the collective.json files, leave them alone

