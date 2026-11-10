---
id: "dc_g9m8xhzcvl"
type: "report"
state: "building"
title: "Redeploy card lists deployed changes with commit links: PR #420 (CI pending)"
authorId: "ag_sjaagna9ex"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #420 (redeploy card lists the deployed changes with commit links) is drafted and green on the desk; the parked continuation as_lvu0lixdz1 waits on its CI, then merges it and lets CI deploy. Goes into rollup #46 with the gr_8cdix9mpye close and the uptime block once those land."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-10T21:02:34.557Z"
sessionId: "se_0gmipw8y9w"
assignmentId: "as_ocyrx9kw0q"
costUsd: 1.5859172
tokens: 79296
turns: 34
createdAt: "2026-11-10T21:02:24.741Z"
updatedAt: "2026-11-10T21:02:34.557Z"
---
## What I did
Built Mitchell's ask from 1:1 mt_db6itzy2br. The redeploy card now lists the changes that went live, not only how many there were. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/420 (commit 8d1ed16a). Checks on my desk: `npm run typecheck` passes, and the runtime (250/250) and web (368/368) tests pass.

## Findings
- **Runtime** (`packages/runtime/src/redeploy.ts`): both pulls now also run `git log --first-parent -n50 before..HEAD`. That covers the first pull and the pull after the drain. The run records two new things:
  - `changes: [{sha, subject}]`, newest first. A GitHub merge commit shows its PR title and (#N). The list holds at most 50; `commits` is still the exact count.
  - `repoUrl`: the repo's https address with any credentials and `.git` removed.
- **Payload field:** **`payload.run.changes`**, plus `payload.run.repoUrl`, on every redeploy system event. Both are written to the done-file, so the restarted server's "finished" event lists them too. An interrupted run's aborted event also carries them.
- **Schema:** two optional fields on `RedeployRun`. Old events still read fine.
- **HUD** (`hud.tsx` and `packages/web/src/redeploy.ts`): the card shows each subject as a line linking to `<repo>/commit/<sha>`. "Log →" still opens the steps. A failed or interrupted run shows no change list, so its steps come first.
- **CI deploys:** the promote job POSTs `/api/admin/redeploy`, so CI deploys go through the same run and their card gets the list too. No fallback at server start was needed.
- I added no CSS rules, to stay within Prod's files plus `hud.tsx`. The list is styled inline instead.
- Next session: once CI is green, merge #420 and let CI deploy it. No `redeploy` call is needed. Then check that the card lists the next deploy's changes.

## What I need from you
Nothing needed.
