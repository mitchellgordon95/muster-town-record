---
id: "dc_xagtsoovg1"
type: "report"
state: "building"
title: "Verified live: the collective repo and the Code access checkbox both work for existing buildings. Nothing was broken; added a round-trip test (main 780c5e7)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:08:20.713Z"
sessionId: "se_31qt0v7997"
assignmentId: "as_00llzsmm97"
costUsd: 0.7832836000000001
tokens: 44556
turns: 33
createdAt: "2026-10-21T00:36:18.778Z"
updatedAt: "2026-10-21T01:08:20.713Z"
---
## What I did
Checked the live town (commit 376ad3f, which includes f050c74) after the redeploy. Nothing was broken. I added an HTTP-level test of the checkbox and pushed it to main as 780c5e7. It's test-only, so I didn't queue a redeploy.

## Findings
- **Migration on live data worked.** `GET /api/town` shows:
  - `town.workspace` holds the repo (`git@github.com:mitchellgordon95/agent-town.git`, base `main`, prefix `agent`).
  - No building has its own `workspace` any more.
- **codeAccess per building:**

  | Building | codeAccess |
  |---|---|
  | Workshop | true |
  | Onboarding | true |
  | Town Hall | false |
  | Prod | false |

  Prod is off because it had no repo before the migration. To give Prod code access, an admin ticks **Settings → Code access**.
- **The full path works end to end:** this session ran on an Onboarding desk with a checkout of the collective repo on my own branch.
- **The checkbox is in the live build:** the served bundle (`index-D8_Kw6sg.js`) contains the "Work on …" / "No collective repo" checkbox and the Overview "Code: the collective repo" row.
- **Toggle effect:**
  - The toggle takes effect on the next session: the brief, the GitHub token and the host-backend refusal all re-read `codeAccess` each time a session starts.
  - Seeding only happens when a town is first created, so a restart won't undo a toggle.
- **What I couldn't test live:** agent tokens can't change building settings (they lack the `building.manage` permission), so I couldn't flip the checkbox on the live town.
- **What I tested instead:** a new test in `packages/server/test/desk.test.ts` takes an existing building with code access off and runs:
  1. The first desk brief has no repo.
  2. The admin sends `PATCH {codeAccess:true}` (what the checkbox saves), and `/api/town` then shows it on.
  3. The next desk brief carries the repo (`https://github.com/o/r.git`).
  4. Switching it off removes the repo again.
- **Checks:** typecheck is clean and all 362 tests pass.
- **Possible concern (not something I broke):** anonymous `GET /api/town` returns `town.workspace.path` (`/Users/mitchg/Desktop/agent-town`) and the desk tool list. Per-building workspaces were exposed the same way before, so this is not new. It may matter for "strangers can trust".

## What I need from you
Nothing needed.
