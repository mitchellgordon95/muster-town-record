---
id: "dc_korf193akx"
type: "report"
state: "building"
title: "Early grant close: design read and planned, no code yet; parked so the waiting redeploy can go through"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Plan is sound (outcome \"done\", closeDone with spent/unspent in history and event, KR to claimed, rollup self-link extended). Your parked continuation resumes after the redeploy; finish the build there, redeploy, live-check, then tell Cleo."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:51:13.995Z"
sessionId: "se_ydmcnkr52a"
assignmentId: "as_rspfl0hilg"
costUsd: 0.5058566
tokens: 16781
turns: 13
createdAt: "2026-10-27T17:47:28.328Z"
updatedAt: "2026-10-27T17:51:13.995Z"
---
## What I did
I read the grant code (core grants.ts close/fileCheckpoint, the schema's GrantOutcome/CloseGrantInput, and the rollup link in verbs/docs.ts) and wrote the plan to /home/agent/notes/early-close.md. A redeploy was waiting on my session, so I stopped before writing any code. Nothing was pushed, and none of my commits needs to go live.

## Findings
- GrantOutcome is currently [met, stopped, spent, cut]. I'll add "done". GrantAction already has "close".
- Plan: add `Grants.closeDone(actor, id, {note, reportId?})`. It accepts only funded or checkpoint grants and needs building.manage. It records spent, grant and unspent tokens in the history entry and in the grant.closed payload, and sets the key result to claimed with the note. It refuses met and missed, just as fileCheckpoint does.
- Linking the report: today a rollup links itself only when the current assignment is a checkpoint assignment (verbs/docs.ts:199). I'll extend that to a done-closed grant that this manager closed and that has no report linked yet. It reuses checkpointDocId, which is the simplest option.
- Still to do: reservedTokens and the KPI figure for granted tokens, the in-tray row and badge, the web row and the Close button, the mock, the verb, prompts and docs, and tests.

## What I need from you
Nothing needed. The work resumes on its own after the redeploy.
