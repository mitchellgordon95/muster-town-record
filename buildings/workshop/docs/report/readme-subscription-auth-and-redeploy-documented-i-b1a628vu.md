---
id: "dc_rvb1a628vu"
type: "report"
state: "building"
title: "README: subscription auth and redeploy documented in two paragraphs (draft PR #35)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:47:15.420Z"
sessionId: "se_woi4b0j7c7"
assignmentId: "as_ywbr53sugr"
costUsd: 0.31518599999999997
tokens: 169296
turns: 8
createdAt: "2026-10-20T04:44:49.995Z"
updatedAt: "2026-10-20T04:47:15.420Z"
---
## What I did
Found that the Run it section already described both topics in one dense **Redeploy** paragraph. I split it into two paragraphs, checked the auth order against the code, read the result back, committed, pushed the branch and opened a draft PR.

## Findings
- PR: https://github.com/mitchellgordon95/agent-town/pull/35 (draft, base main). It changes only `README.md`.
- **Redeploy** paragraph: `scripts/serve.sh` restarts the server when it exits with code 75. The `redeploy` verb, the planning-desk button, and `POST /api/admin/redeploy { image? }` all pull main, rebuild the client, and rebuild the desk image when `image: true`. Anyone with the `deployer` role or admin can use it.
- **Subscription auth** paragraph (new): `CLAUDE_CODE_OAUTH_TOKEN` in `<collective>/.env` (from `claude setup-token`). The order is donor API key, then the OAuth token, then `ANTHROPIC_API_KEY`. This matches `packages/runtime/src/desk/session.ts:46-52`.
- Checked by reading README lines 24–30 back after the edit. It's docs only, so I didn't run typecheck or tests.

## What I need from you
Nothing needed.
