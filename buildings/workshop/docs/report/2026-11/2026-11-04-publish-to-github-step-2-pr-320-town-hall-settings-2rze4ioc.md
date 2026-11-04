---
id: "dc_9z2rze4ioc"
type: "report"
state: "building"
title: "Publish to GitHub step 2: PR #320 (Town Hall Settings block) open, parked on CI"
authorId: "ag_vyjvfz0eos"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:54:51.496Z"
sessionId: "se_9y03dplte2"
assignmentId: "as_wzb2vwhlzv"
costUsd: 0.8233102999999999
tokens: 41166
turns: 21
createdAt: "2026-11-04T18:31:13.090Z"
updatedAt: "2026-11-04T18:54:51.496Z"
---
## What I did
I built the web half of kr_gyqktjpevz on top of step 1, which is merged (5baee1d). The work is in draft PR https://github.com/mitchellgordon95/muster-town/pull/320. `npm run check` passed locally in the foreground: 70 web test files and 314 tests. The PR adds no migration. I've parked the session on {pr: 320}.

## Findings
- **Settings block:** Town Hall → Settings, under "Collective defaults" and visible to admins only, now has a "Publish to GitHub" block (`PublishToGitHub` in BuildingPanel.tsx):
  - A repo URL input.
  - A password-type token field. It never shows the token; its placeholder says either "not set" or "set (leave blank to keep it)".
  - A hint explaining that the token needs Contents read/write, is kept encrypted, and is never shown again.
  - Save, which calls PUT. It is disabled until there is a repo URL, and also until there is a token when none is stored yet.
  - Clear, which asks for confirmation, then calls DELETE. It only appears once publishing is set.
  - A last push line, which reads one of "Last push: <ago> · <commit7>", "Last push failed: <error>" (in red) or "No push yet: the next hourly export pushes."
- **Errors:** server errors such as 409 NO_DATA_KEY or 400 for a bad URL appear inside the block, not only as a toast.
- **No reload needed:** `store.town.publish` is updated from the server's reply, so the line refreshes straight away.
- **API client:** api.ts has `publishSettings({repoUrl, token?})` and `clearPublish()`, plus mock implementations. A hosted World uses the same block through its /<slug> prefix.
- **Test:** packages/web/test/publishToGitHub.test.tsx covers the line text in each state, the set / not set placeholder, and rendering with and without publishing set.
- **Next session:** if CI is green, merge, redeploy and park on {deploy: sha}. Then check the live Town Hall Settings block and rewrite topic page [dc_0ub741sboo](../../wiki/2026-11/2026-11-04-publish-to-github-gr-30f8obzab8-b741sboo.md) with the step 2 state. That page is not rewritten yet because nothing is merged.

## What I need from you
Nothing needed.
