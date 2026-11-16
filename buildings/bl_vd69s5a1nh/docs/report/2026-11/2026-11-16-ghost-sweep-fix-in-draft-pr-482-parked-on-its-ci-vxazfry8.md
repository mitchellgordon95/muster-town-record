---
id: "dc_bzvxazfry8"
type: "report"
state: "building"
title: "Ghost sweep fix in draft PR #482; parked on its CI"
authorId: "ag_h9x8n9z95l"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Draft PR #482 (ghost sweep keeps visitors holding a town-scope role other than role:visitor, e.g. the CI deployer's \"deployer\" role per deploy/README.md:41; Presence.seen stamps lastSeenAt on agent-bearer REST calls) is parked on its CI as as_13iujxoqej, which marks ready and merges on green. Nothing new queued. The remaining need (a new CI deployer visitor + MUSTER_TOWN_DEPLOY_TOKEN secret) is already with Mitchell as credential ask ak_tlets696sj, and a one-off redeploy click as ak_nugzl9rheu; no second ask filed."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-16T19:48:44.226Z"
sessionId: "se_byze51r7r1"
assignmentId: "as_307jrox6sv"
costUsd: 1.1546933000000001
tokens: 57735
turns: 27
createdAt: "2026-11-16T19:48:24.428Z"
updatedAt: "2026-11-16T19:48:44.226Z"
---
## What I did
Fixed the ghost-visitor sweep so it no longer retires the CI deployer visitor. The fix is in draft PR #482 (https://github.com/mitchellgordon95/muster-town/pull/482), branch agent/mara-2/fix-the-ghost-visitor-sweep-must-not-ret. Pix (Workshop) has no open fix PR, so there was nothing to fold into.

## Findings
- **Pure rule.** `ghostVisitors(agents, managerIds, roleHolderIds, nowMs)` now also keeps visitors in `roleHolderIds`. `keepsVisitor(roleId)` keeps a town-scope role (`role:<name>`) other than `role:visitor`. This matters because every visitor agent holds `role:visitor` (entities.ts:322), so keeping "any town role" would have kept every visitor. `Presence.retireGhosts` builds the set from `memberships.forHolder` for the offline visitors only.
- **REST presence.** New `Presence.seen(agentId)` stamps `lastSeenAt` and does nothing else. It uses the same STAMP_EVERY_MS throttle as `touch` (one silent upsert per agent per 10 s at most) and runs no "back" transition, so bodies and status do not move. The server calls it from an `onResponse` hook for any agent-bearer request. It runs after the handler on purpose: an MCP or verbs `touch` of an offline visitor still reads the old `lastSeenAt` for its digest window. An offline REST-only visitor stays at the bench, but it is no longer quiet to the sweep.
- **Docs.** Invariant 12 in docs/invariants/agent-lifecycle.md now names both rules and three tests. The log line is in docs/log.d/2026-11-16-mara-2-ghost-sweep-keeps-deployer.md.
- **Tests.**
  - core ghost-visitors.test.ts: the property test with role holders, a `keepsVisitor` table, a deployer visitor never retired with its token kept, and `seen` stamping without the back transition.
  - server presence-seen.test.ts: a plain GET /api/me by an offline visitor stamps `lastSeenAt` and leaves it offline.
- **Checks.** Typecheck, docs and knip passed. In the full `npm run check`, 332 of 333 tests passed. The one failure was `backup.test.ts` › "runs in a worker thread", a timing test already listed on the topic page as a desk flake; it is unrelated to this change.
- **What this does not fix.** The CI visitor already dismissed stays retired and its token stays revoked. CI's promote keeps getting 401 until a human makes a new deployer visitor and puts its token in the MUSTER_TOWN_DEPLOY_TOKEN Actions secret (deploy/README.md:399).
- **Live check, once this is live.** A deployer-role visitor survives the sweep's next pass, and its `lastSeenAt` moves on each CI redeploy call.

## What I need from you
Nothing for this PR yet. Separately, a human must re-make the CI deployer visitor and update the MUSTER_TOWN_DEPLOY_TOKEN secret, or no merge goes live, including this one.
