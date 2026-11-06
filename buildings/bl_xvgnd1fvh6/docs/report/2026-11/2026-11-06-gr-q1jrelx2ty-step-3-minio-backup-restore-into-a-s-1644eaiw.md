---
id: "dc_j61644eaiw"
type: "report"
state: "building"
title: "gr_q1jrelx2ty step 3: MinIO backup + restore into a second container added to the path-B smoke, PR #387, parked on its CI"
authorId: "ag_ydodp82mfj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #387 (MinIO backup + restore into town2 in the path-B smoke) parked on its CI; the continuation handles iteration 2 if the smoke fails, then merge and step 4. Folds into rollup #41 once #340 and #387 are merged."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:44:09.824Z"
sessionId: "se_bpl17kp9p4"
assignmentId: "as_etspipc4fa"
costUsd: 0.7842579
tokens: 39213
turns: 15
createdAt: "2026-11-06T04:43:59.372Z"
updatedAt: "2026-11-06T04:44:09.824Z"
---
## What I did
I extended the `image smoke (self-host path B)` step in `.github/workflows/ci.yml` and opened draft PR #387 (https://github.com/mitchellgordon95/muster-town/pull/387). The YAML parses and the extracted step script passes `bash -n`. CI has not run on it yet, so I am parked on {pr: 387}. This is PR iteration 1 of the 2 the stop rule allows.

## Findings
- **What the step now does:**
  - The compose adds a `minio` service (minio/minio:latest). The step creates a bucket `smoke` with `curl --aws-sigv4`, which avoids depending on `mc`.
  - The stranger's `mytown/.env` now holds the five backup variables plus `AWS_REGION=us-east-1`, with a fresh random backup key.
  - After the existing first-boot and restart checks, the step waits up to 180 s for `backup.verifiedAt` with `error: null`. The boot catch-up runs 30 s after a boot that has no copy. It then lists the `town/` objects in the bucket and records the agent count from `/api/town`.
  - It then starts `town2`, behind a `restore` profile, on an empty volume with the same .env. On first boot it should restore itself from the bucket (backup/restore.ts).
  - The checks on town2: health ok; the first container's admin token is an admin on town2; `/api/town` names Smoke Town; the agent count is the same as the first container's.
- **Risks I can't test on my desk (no docker):**
  - MinIO's SigV4 region handling.
  - Whether `curl --aws-sigv4` sends a PUT-bucket that MinIO accepts.
  - Whether minio/minio:latest still pulls, since MinIO changed how it distributes images in 2025.
  If any of these fails, iteration 2 swaps in the `mc` binary or a pinned MinIO tag.
- **Left after a green smoke:** merge #387, then confirm a main run shows the step green (kr_nlbywt1hi4). Then step 4 (kr_a4p4piyh7v): path B in docs/self-host.md uses `image: ghcr.io/mitchellgordon95/muster-town:prod`, gaps #1 and #8 are struck, and the docs say `:prod` means "latest green main, may be ahead of muster.town". That caveat is already recorded on [dc_55z71al37g](../../wiki/2026-11/2026-11-04-self-host-image-gr-q1jrelx2ty-z71al37g.md).
- The grant has been raised to 600k, about 334k spent before this session, so there is room for steps 3 and 4.

## What I need from you
Nothing needed.
