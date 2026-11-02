---
id: "dc_zr0j3q0oe9"
type: "report"
state: "building"
title: "Model picker verified on live 34cc56c; desk clone works now"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-23T04:30:30.510Z"
sessionId: "se_ltrgl9f64k"
assignmentId: "as_a7d8kr769y"
costUsd: 0.3637691999999999
tokens: 14479
turns: 16
createdAt: "2026-10-23T04:30:17.392Z"
updatedAt: "2026-10-23T04:30:30.510Z"
---
## What I did
I confirmed the workspace clone worked this session and checked the model picker API on the live build (/api/health commit 34cc56c, which contains 12a1a89). I tested it as a non-manager agent and with no token, read the model-change events, and reran the core unit test. I made no code changes, so there's no commit and no redeploy.

## Findings
- **Clone credentials are fixed.** This session's checkout cloned without errors and `GH_TOKEN` is set in the desk env. The earlier failure ([dc_01l7i4zggj](2026-10-23-session-ended-without-a-report-verify-the-model-pi-l7i4zggj.md)) was `fatal: could not read Username for 'https://github.com': No such device or address`. That means no credentials were supplied at all; it wasn't GitHub rejecting a token. I told Pix this, since Pix asked in the standup.
- **Owner path works live.** The event log shows Mitchell (us_1la74k332n, owner of all four residents) used the picker on 2026-10-21: Pix → claude-fable-5-1 at 04:11:22Z, then Lena → claude-haiku-5-5 → claude-opus-5-5 at 04:11:45–50Z. This session runs on claude-opus-5-5, which shows the picked model reaches the work session.
- **Permission checks hold.** My agent token has no building.manage: `PATCH /api/agents/ag_oycvqt9sa6/model` returned 403 "you need the building.manage permission", and `GET /api/agents/:id` reports `canSetModel: false` for every resident. With no token the same call returns 401.
- **Manager path is only partly checked.** Pix is the only agent with building.manage, and agents have no town tool for setting a model, so nobody has run a manager PATCH live. It is covered by `packages/core/test/agent-model.test.ts` ("a manager sets and clears a resident's model; a stranger can't"), which passes (2/2). A live check needs a human manager who isn't the owner or an admin, and as far as I know none exists today.

## What I need from you
Nothing needed.
