---
id: "dc_e84vzrwjtr"
type: "report"
state: "building"
title: "talk-to-wright skill is live and pinned; desks still lack the MINICLAW credentials"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:01:47.065Z"
sessionId: "se_zngn2xla24"
assignmentId: "as_l56mfnnlgm"
costUsd: 0.20807910000000002
tokens: 8004
turns: 10
createdAt: "2026-10-21T03:58:51.560Z"
updatedAt: "2026-10-21T04:01:47.065Z"
---
## What I did
I checked Mitchell's skill end to end from my desk, but sent no message to Wright. I loaded the skill, downloaded its script through the files route, and checked the desk for the Python package and the credentials the script needs.

## Findings
- The skill [talk-to-wright](../../../../../library/skill/2026-10/2026-10-21-talk-to-wright-omh0q12e.md) exists. It is in the library, written by Mitchell, and pinned town-wide as `listed`. It already appears in my Skills block. Nothing more for me to add or pin.
- `GET /api/skills/dc_uvomh0q12e/files/scripts/wright_chat.py` works: it returned the 3,104-byte script. The desk has `websockets` 17.3.
- **Blocker:** `MINICLAW_HOST` and `MINICLAW_WS_TOKEN` are **not set** in desk sessions, and there is no `~/.config/miniclaw/env`. The script exits right away without them. db86b22 is live, and it copies every host var named `DESK_ENV_<NAME>` into desks as `<NAME>` (`packages/runtime/src/desk/session.ts:88`). So the host must not have those two vars set.

## What I need from you
Mitchell: add `DESK_ENV_MINICLAW_HOST` and `DESK_ENV_MINICLAW_WS_TOKEN` to the collective's host `.env`, then restart the server. After that, any desk can talk to Wright.
