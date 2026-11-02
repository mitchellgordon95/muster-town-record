---
id: "dc_qcczz8gjhd"
type: "report"
state: "building"
title: "One repo per collective: buildings get a Code access toggle instead of their own repo (main f050c74, redeploy queued)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T22:17:29.861Z"
sessionId: "se_bof2ssdvbs"
assignmentId: "as_qczhi9m49k"
costUsd: 2.1186182
tokens: 149569
turns: 62
createdAt: "2026-10-20T22:08:28.766Z"
updatedAt: "2026-10-20T22:17:29.861Z"
---
## What I did
Answered Mitchell's question ("should we even have building-level repos?" No), then made the change. The repo now belongs to the collective, and each building has an on/off code-access toggle. Pushed straight to main as f050c74 under the Onboarding standing rule, so there's no PR. Redeploy is queued.

## Findings
- **Before:** each building stored its own `workspace` with a host path and repo URL. The Settings tab showed it as a greyed-out host path. Buildings created from the planning desk had no repo at all, so they had no code access.
- **Now:**
  - The collective's repo is stored on the town (`Town.workspace`). It comes from the top-level `workspace` in `collective.json`.
  - Buildings have a `codeAccess` flag. New buildings get it automatically when the collective has a repo; Town Hall never does.
  - Desk briefs, the GitHub token, host-backend refusal, proxy chat and the deployer-role fix all read the repo through one helper, `codeWorkspace(town, building)`.
- **Migration 022:**
  - Adds `buildings.codeAccess` and turns it on for every building that had a workspace, so Workshop and Onboarding keep code access.
  - Moves the first building workspace up to the town if the town doesn't have one yet.
  - On restart, seed sets the collective repo from `collective.json` if the town still has none.
- **UI:**
  - The Settings tab now has a **Code access** checkbox labelled "Work on `owner/repo`", with a hint that every building shares the one collective repo.
  - Overview shows a "Code: the collective repo …" row.
  - Screenshot checked against the mock server.
- **Verified:**
  - `npm run typecheck` is clean.
  - All 373 tests pass across the packages, after rebasing onto Kelly's 41a77db.
  - New tests cover the migration lifting the repo to the town, `codeAccess` defaults at seed, the repo backfill on restart, and the GitHub token and host refusal for buildings with code access.
- `collective.json`, README, architecture and design docs, and `docs/log.md` are updated.

## What I need from you
Nothing needed.
