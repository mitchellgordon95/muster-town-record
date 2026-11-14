---
id: "dc_9sp6jxhvtp"
type: "report"
state: "building"
title: "Image deploy live; it broke host sessions (SDK unresolvable from dist), fix PR #449 parked on CI"
authorId: "ag_qqi4nzbopb"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #449 merged and is live: health commit 5a7e229, startedAt 23:47:21Z (this manager session itself is a host session that started). Continuation as_4brh99u6gh is confirming host sessions and boot timings."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-13T23:48:10.588Z"
sessionId: "se_o5l4t0grws"
assignmentId: "as_md46zbpczz"
costUsd: 0.9338779000000001
tokens: 46694
turns: 22
createdAt: "2026-11-13T23:30:25.864Z"
updatedAt: "2026-11-13T23:48:10.588Z"
---
## What I did
- Checked the image deploy Mitchell ran ([dc_lpit4t3uby](../../../../../library/human-report/2026-11/2026-11-13-re-run-deploy-fly-build-sh-once-town-image-deploy-it4t3uby.md)) against /api/health and /api/events.
- Found and fixed a regression it exposed: PR https://github.com/mitchellgordon95/muster-town/pull/449.
- Posted town FYI [dc_00d41j6bl0](../../../../town-hall/docs/fyi/2026-11/2026-11-13-host-sessions-secretary-managers-fail-since-the-23-d41j6bl0.md) and updated topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md).

## Findings
- **The deploy landed.** "Server started" was logged at 23:19:37Z (event 155900) and health startedAt is 23:19:39Z. The commit is still 543af33. Backup was ok at 23:00Z. The server now runs the prebuilt bundle: error paths point at /data/repo/packages/server/dist/chunk-*.js.
- **Regression: every host session fails at once.** The error is "Cannot find package '@anthropic-ai/claude-agent-sdk' imported from /data/repo/packages/server/dist/chunk-WLTX33Z3.js" (event 155923).
  - The SDK was installed only in packages/runtime/node_modules and packages/desk/node_modules, and Node can't find it from packages/server/dist.
  - The Secretary crash-loops every 5 s: about 100 failed sessions by 23:27Z. Mitchell's 1:1 mt_5is8stmjvo is dead. Manager in-tray sessions are affected too. Desk forks (docker) work.
- **PR #449 fixes it.** packages/server now declares the SDK, and the lockfile hoists it to the root at the same 0.3.304. A plain `npm install` had bumped it to 0.3.325, so I pinned it instead. build.mjs now exits 1 when any external can't be found from dist, so start-server.sh falls back to tsx rather than run a broken bundle.
  - Checked on a desk: the build is ok and the SDK imports from dist. With the SDK hidden, the build fails and names it. Typecheck is green.
  - The live redeploy runs npm install because the lockfile changed, so CI's normal ship applies the fix.
- **Boot time:** the "after" number for a restart on the bundle waits for the next CI redeploy (tsx baseline 3.1 s).

## What I need from you
Nothing needed. I resume on #449's CI and merge it on green, which is the fastest way to bring the Secretary and managers back.
