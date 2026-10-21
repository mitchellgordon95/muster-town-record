---
id: "dc_mi7y4wdlts"
type: "report"
state: "building"
title: "Town-picked resident names + 3 starter residents for new buildings (on main, redeploy queued)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T22:17:12.101Z"
sessionId: "se_0pv666jqya"
assignmentId: "as_das0ru2tjn"
costUsd: 1.0615740999999999
tokens: 1803347
turns: 39
createdAt: "2026-10-20T21:51:21.770Z"
updatedAt: "2026-10-20T22:17:12.101Z"
---
## What I did
The block is gone and my desk now has a repo checkout. I did the planned names and seeding work, pushed it to main as commit 41a77db (my branch matches main), and queued a redeploy. I told Craig which API to use for the reroll button in his form.

## Findings
- **Name generator:** `packages/core/src/names.ts` has a list of 70 short first names (`RESIDENT_NAMES`). `suggestResidentName` picks one at random that no agent in the town already uses, ignoring case. When every name is taken it adds a number, like "Lena 2".
- **No name needed:** `CreateResidentInput.name` is now optional. If it's left out or blank, the town picks the name.
- **Reroll:** `GET /api/agents/name-suggestion?avoid=a,b` returns `{name}` and skips the names you pass in `avoid`. The web API exposes it as `suggestName()`, and the mock server supports it too.
- **Seeding:** a new building made through `POST /api/buildings` or the planning desk now starts with 3 residents. The first one is set as the building's manager, and the count is capped by headcount. Buildings created from config or imports are unchanged.
- **Checks:** typecheck passes, and all tests in every package pass (core 182, server 56). I added `core/test/starter-residents.test.ts` and checks for the new endpoint in `rest.test.ts`. I changed two tests that assumed a new building starts empty: in one the building is now full, so I raised the other's headcount from 4 to 5. `docs/architecture.md` and `docs/log.md` are updated.
- **Not done:** the starter residents only get `managerAgentId`. They don't get the building's `manager` role, so they can't assign work. The NewResident form in the building settings panel still asks for a name; Craig is building the version with the reroll button.

## What I need from you
Nothing needed.
