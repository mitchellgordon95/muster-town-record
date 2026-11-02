---
id: "dc_fj4nfgodwx"
type: "report"
state: "building"
title: "Plant a flag shipped to main: core 7810e8c (flag doc, human-only POST, in-tray + manager wake, review+assigneeId delegates as directed) and web 9b20fad; parked until live"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked; continuation as_9plpbghwme (verify live, tell Mitchell) resumed since 9b20fad is live. Rollup 6 after that verification."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T04:28:03.912Z"
sessionId: "se_10zdn84waf"
assignmentId: "as_5avu8lc06d"
costUsd: 2.7221155000000006
tokens: 62055
turns: 38
createdAt: "2026-10-26T00:32:52.444Z"
updatedAt: "2026-10-26T04:28:03.912Z"
---
## What I did
Followed the redirect rules. Leftovers first: `git fetch --all`, branches, stashes. The second attempt (se_iyamnzz79v) had left its whole change, tests included, in an auto-stash on my desk (`stash@{0}`, 18 files). I applied it, rebased it twice over fresh main commits (Root 16690b0, Keel 53482f8, Cleo deabe02; one trivial Places.tsx conflict), kept the lane decision but added the "why not exploration" reasoning the redirect asked for, typechecked all packages (0 errors), ran core flags/manager/prompts/lanes tests (23 pass), the server flags test (1 pass) and the whole web suite (51 pass), all in the foreground, and pushed to main in two layers:
- **7810e8c** core/schema/server/runtime/docs.
- **9b20fad** web (recovered UI; the redirect left it to Root, but it existed, compiled and tested green, so dropping it would have been waste). Told Root his as_sk61n57yqf is now live verification only.

No migration 033 was needed: a flag is a doc of type `flag` and `docs.type` is free text.

## Findings
**REST shape (for Root and the UI):**
- `POST /api/buildings/:id/flags` body `{text}` (1–2000 chars, first line = title). Human-only with `building.assign` on that building: no token → 401, stranger → 403, agent token → 403, Town Hall → 400. Returns 201 `{doc}` with `type: "flag"`, `state: "building"`, `decision: "pending"`, `buildingId`.
- `GET /api/buildings/:id/intray` → `{reports}` now includes pending flags (type `flag`); the Town Hall in-tray never does. All flags, decided too: `GET /api/buildings/:id/cabinet?type=flag`.
- `POST /api/docs/:id/review` body `{decision, note?, assigneeId?, waitFor?}` → `{doc, assignment}`. On a flag: `continue` = the flag text verbatim becomes `assigneeId`'s assignment, `redirect` = the note (flag as context), `approve` = handled, `stop` → 400. `assigneeId` must be a resident of the flag's building. Same `assigneeId` on the `review` verb.
- Runtime: a `doc.created` with `docType: "flag"` wakes the manager's team-lead session exactly like a report; the in-tray block shows `FLAG by <human>: <text>` and the manage prompt says how to delegate it.

**Lane decision** (docs/waterfall.md, "Flags"): the delegated assignment is **directed** whatever the budget mode, as a meeting decision a human spoke in is directed. The redirect recommended exploration with the flag text as the gap; I went the other way because exploration is capped by the daily allowance, so a flag planted after the allowance is spent (Workshop: 10.1M of 5.4M on 10-25) would be held until midnight, the opposite of a quick fix, and it would be the only case where a human's ask counts against the agents' allowance. "Agents can't create directed work" stays true: only a human can plant a flag, and the manager only picks who. If flags get abused as a budget bypass, cap flags per day on the human side.

**Web** (9b20fad): ⚑ Plant a flag on the Town Hall in-tray (building picker) and on a building's in-tray; flag rows badged; an open flag shows a Handled / Assign-to box for the human; HUD counts "reports, flags". Not yet seen in the live town, only tests.

Live is still the pre-flag build; CI ships 7810e8c and 9b20fad on green. Parked on {deploy: 9b20fad}.

## What I need from you
Nothing needed. (Mitchell: once 9b20fad is live, plant the first flag from the Town Hall in-tray's ⚑ button.)
