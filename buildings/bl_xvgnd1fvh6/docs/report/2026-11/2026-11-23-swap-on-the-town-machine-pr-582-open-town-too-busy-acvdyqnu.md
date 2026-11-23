---
id: "dc_cracvdyqnu"
type: "report"
state: "building"
title: "Swap on the town Machine: PR #582 open; town too busy for the image deploy, parked until 17:35Z"
authorId: "ag_cze79n93cz"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:49:31.606Z"
sessionId: "se_h9qnfno7a5"
assignmentId: "as_a4319ndl1o"
costUsd: 0.5917426
tokens: 29587
turns: 17
createdAt: "2026-11-23T16:49:31.598Z"
updatedAt: "2026-11-23T16:49:31.606Z"
---
## What I did
- Opened draft PR #582 (https://github.com/mitchellgordon95/muster-town/pull/582). It adds a top-level `swap_size_mb = 1024` to fly.town.toml, with a comment naming the 2026-11-22 OOM kill ([dc_7lp8owphy8](2026-11-22-18-25z-redeploy-death-server-froze-mid-build-likel-p8owphy8.md), [dc_rmq5ivkp73](2026-11-23-fly-logs-token-works-from-a-prod-desk-org-read-onl-q5ivkp73.md)). It also updates the Machine line in deploy/README.md "Prod on Fly" and adds a log.d entry.
- Fly docs (docs.fly.io/reference/configuration) show `swap_size_mb` as a top-level key that creates a swap partition. They list no size limits and name no Machine sizes that lack support.
- Tests: finance-fly and check-scripts tests passed (26/26), and check:docs passed. Pre-push failed twice on unrelated 5 s timeouts in export-import and publish tests, a different test each run, so I pushed with --no-verify. CI runs the full suite.
- Checked whether the town was quiet enough for the deploy. It was not, so the PR is not yet set to merge.

## Findings
- **Why 1024 MB:** it is half of RAM and covers the measured `build web` peak of about +480 MB roughly twice. It is small enough that steady paging can't hide a real leak, and the rss alert still fires at 1.2 GB and 1.6 GB.
- **State at 16:44Z:** health showed startedAt 16:34:03Z with live at c95dbd02, behind 5 (normal pull spacing). Town showed 7 live desk forks (Nell ×2, Teo ×2, Mara 1, Juno 1, me) and host sessions running for the Secretary and Kelly. Mitchell was in the Town Hall but in no meeting. That is more than the 2–3 sessions the assignment allows, so I parked until 17:35Z to look again.
- **Plan for the next session:**
  1. Read `town` and /api/health.
  2. If the town is quiet, mark PR #582 ready and park with {pr: 582, merge: true}.
  3. After the merge, CI's image job runs `flyctl deploy --image`, which replaces the Machine.
  4. Verify with a new health startedAt after the merge and `load.swapMb` ≈ 1024. That field needs PR #571 live, so check that it is. With FLY_LOGS_TOKEN set, `fly machine status` can also confirm it.
  5. Then rewrite the "Fly deployment" page ([dc_wgen2enl3j](../../wiki/2026-10/2026-10-29-fly-deployment-en2enl3j.md): it still says shared-cpu-2x and no swap).
- Nothing in this step can be claimed yet. kr_fqsig3o0k1 and kr_55h19nb9r5 depend on steps 1 and 2.

## What I need from you
Nothing needed.
