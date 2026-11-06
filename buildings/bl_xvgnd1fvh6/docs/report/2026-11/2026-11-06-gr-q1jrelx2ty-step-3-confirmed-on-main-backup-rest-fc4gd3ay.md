---
id: "dc_wkfc4gd3ay"
type: "report"
state: "building"
title: "gr_q1jrelx2ty: step 3 confirmed on main (backup + restore green, image on ghcr); step 4 docs in PR #392, waiting on its CI"
authorId: "ag_gyp1brh5t6"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "gr_q1jrelx2ty step 4 (final): PR #392 (docs/self-host.md path B pulls ghcr.io/mitchellgordon95/muster-town:prod; docs only) has finished CI. If green: mark it ready and merge it to main (docs-only, so CI moves `prod` without a restart; do NOT call redeploy). Then confirm on GitHub that the main run for the merge commit is green (or still queued: say so, it does not block a docs change), and read docs/self-host.md on main to confirm path B reads as in dc_wkfc4gd3ay. Claim kr_a4p4piyh7v with keyResults evidence (the merge commit sha, the file path, the ghcr tags :prod and :<sha> that match digest sha256:704e1364…). Then run close_grant gr_q1jrelx2ty with a note a human can check (the main run id 42166369737 where restore-into-town2 passed, the ghcr tags, the merged docs), and submit_report with rollup: true as its close report: ## Shipped with one item (the published image + first-boot restore + the self-host path B, What it is / What you'd see / Your call: \"Close gr_q1jrelx2ty as done: X of 600,000 spent; Y returned\" — or none), ## Decided (dc_wkfc4gd3ay → redirect, plus your own report), ## Key results (gr_q1jrelx2ty's rows with status and spent/granted; other grants one line each), ## Needs from Mitchell: nothing unless the merge itself was refused. Keep the close rollup to this grant: Prod rollup #41 (separate) covers the rest of the building. If CI is red: fix only what the docs lint complains about, push, and park on {pr: 392} once (this chain's parks reset with the new assignment); if it is something you can't fix, report with verdict pivot and say what. Update topic page dc_55z71al37g and the wiki pages you touch."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T05:27:40.983Z"
sessionId: "se_ik4p6vorf9"
assignmentId: "as_j8uzjz9vif"
costUsd: 0.8467468
tokens: 42337
turns: 18
createdAt: "2026-11-06T05:26:50.454Z"
updatedAt: "2026-11-06T05:27:40.983Z"
---
## What I did
- **Main confirmation.** Main run 42165470594 (5498fd86) was cancelled because newer pushes landed behind it in the queue. The next green main run is 42166369737 on 24984fc6, which contains 5498fd86. In that run, check, image (smoke + push) and promote all passed. 24984fc6 is live on muster.town.
- **Step 4 (kr_a4p4piyh7v).** I rewrote path B in docs/self-host.md to pull the published image and opened draft **PR #392** (https://github.com/mitchellgordon95/muster-town/pull/392). It changes docs only.
- I could not park on its CI: the chain has already parked 3 times in a row. **I'm waiting on PR #392's CI.** Next: an assignment with waitFor {pr: 392} that merges it on green, claims kr_a4p4piyh7v, then runs close_grant gr_q1jrelx2ty with a rollup.

## Findings
- **Main-run smoke log, run 42166369737** (runner UTC):
  - A backup was verified at 05:11:12Z (34,448 bytes, error null).
  - `town2` booted on an empty volume and logged `[restore] town/2026-11-06T05.db.gz.enc: ok, 3 agents`.
  - town2 came back as Smoke Town with 3 agents, and the first town's admin token works on it.
- So kr_nlbywt1hi4 holds on main as well as on the PR run.
- **ghcr, checked anonymously.** `:prod` and `:24984fc62ed5…` have the same digest (sha256:704e1364…). `:5498fd86…` returns 404: a main run that gets cancelled never pushes its `:sha` tag. Every completed green main run does push one, so `:<sha>` exists only for commits whose run finished.
- **PR #392 changes to docs/self-host.md:**
  - Path B's compose uses `image: ghcr.io/mitchellgordon95/muster-town:prod`, with no clone or build.
  - It explains that `:prod` is the latest green main and can be ahead of muster.town, and says to pin a `:<sha>` tag for an exact commit.
  - It says CI boots this exact compose before every push.
  - Section 5 documents first-boot restore: an empty volume plus the backup variables restores the town from the bucket.
  - Upgrades: `docker compose pull` alone does not replace `/data/repo`.
  - Known gaps #1 and #8 are struck through, citing PRs #310, #342 and #387.
  - Gap #4 is narrowed to what is still untried: a real domain with TLS, GitHub sign-in, a Docker desk session, and a real S3 provider other than Tigris. CI's moto bucket does not check request signatures.
  - Building your own image stays as a short note for forks.
- The topic page [dc_55z71al37g](../../wiki/2026-11/2026-11-04-self-host-image-gr-q1jrelx2ty-z71al37g.md) is updated.

## What I need from you
Nothing needed.
