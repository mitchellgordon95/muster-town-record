---
id: "dc_s5dnke33g7"
type: "report"
state: "building"
title: "Publish to GitHub step 1: PR #313 (per-World repo + token, export pushes, health.export), parked on CI"
authorId: "ag_37dkgy1g8p"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by dc_72l4hnnqwp (PR #313 merged as 5baee1d)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:26:33.824Z"
sessionId: "se_bp1gqjtorf"
assignmentId: "as_lo8ritvcl9"
costUsd: 2.183540600000001
tokens: 109177
turns: 38
createdAt: "2026-11-04T18:13:56.550Z"
updatedAt: "2026-11-04T18:26:33.824Z"
---
## What I did
Built step 1 of gr_30f8obzab8 (the API side and the push) as one draft PR: https://github.com/mitchellgordon95/muster-town/pull/313 (branch agent/pix-2/publish-to-github-step-1-gr-30f8obzab8-p, off edb3201). I ran typecheck and the core, server and runtime tests locally, in the foreground, and all passed. I rewrote topic page [dc_0ub741sboo](../../wiki/2026-11/2026-11-04-publish-to-github-gr-30f8obzab8-b741sboo.md) with the routes and field names so step 2 (the web block) can start from it. This session is parked until PR #313's CI finishes.

## Findings
- **Setting (one per World, no migration):** `Town.publish {repoUrl, tokenSet, lastPushAt, lastPushCommit, lastPushError}` is stored in the town meta row. `GET /api/town` and the snapshot include it. Neither ever includes the token.
- **Token:** stored as a runtime-owned secret, `MUSTER_TOWN_PUBLISH_TOKEN`, written through new `Secrets.setOwn`, `clearOwn` and `hasOwn`. It is hidden from `list`, `get` and `forAgent`, so no desk can ever receive it. Through `/api/secrets`, PUT gets a 400 and DELETE answers `{removed:false}`. Saving a token on a host with no data key gets a 409 NO_DATA_KEY.
- **API (only an admin of that World; agents and non-admins get 403):**
  - `PUT /api/town/publish {repoUrl, token?}` returns `{publish}`.
  - `repoUrl` must look like `https://github.com/<owner>/<repo>`, with or without `.git`; anything else gets a 400.
  - Leaving out the token keeps the stored one. A new URL or token resets the lastPush* fields.
  - `DELETE /api/town/publish` returns `{cleared}`.
  - Events `town.publish-set` and `town.publish-cleared` never carry the token.
- **Push:**
  - `World.exportOffThread` passes the World's own `publishTarget()` to the worker.
  - `writeExport` runs `git push -q -- <url> HEAD:refs/heads/main` whenever HEAD differs from the last pushed commit. That covers a new commit, and also catching up after a failed push when nothing changed locally.
  - The token goes only into that one git call's environment as an `http.extraheader`. It is never in argv, the remote URL or `.git/config`.
  - The push is **not forced**, so the GitHub repo must start empty. A repo created with a README will reject the push, and the error shows.
  - A failed push never fails the export: the local commit still lands.
  - `ExportResult` and the `export.done` payload gain `pushedAt`, `pushCommit` and `pushError` (git's first line, with tokens masked). `World.recordExport` appends the event and writes the lastPush* fields; the runtime now calls it.
- **Health:** `GET /api/health` now includes `export: {lastAt, commit, lastPushAt, pushError}`. A hosted collective reports its own at `/<slug>/api/health`.
- **Tests:**
  - New core file `test/publish.test.ts`, 7 tests. It pushes to a local bare repo over file://. It checks the token appears nowhere: not in the export dir, the bare repo, `.git/config`, the result or the event. It also covers a bad URL (the export still commits and the error is masked), the worker path with a failure followed by recovery, and two Worlds each pushing only their own `town.json` (kr_sqbsdpaju8).
  - New server file `test/publish.test.ts`, 2 tests: the routes as admin, agent, non-admin user and guest; the token never in any response; the 409; `health.export`.
  - Full suites: core 734/734, server 281/281, runtime 221/221.
- **Docs:** `docs/secrets.md` (the publish token) and `docs/architecture.md` "Export" (a Publish to GitHub paragraph).
- **Step 2 (web):** add a Publish to GitHub block to the Town Hall Settings, next to "Collective defaults". It needs a repo URL field, a write-only token field, Save (PUT), Clear (DELETE), a last-push line read from `town.publish`, and an "use an empty repo" hint. The details are on [dc_0ub741sboo](../../wiki/2026-11/2026-11-04-publish-to-github-gr-30f8obzab8-b741sboo.md).

## What I need from you
Nothing needed now. For the live check (step 3), Mitchell will need an **empty** GitHub repo and a fine-grained token with Contents read/write on it.
