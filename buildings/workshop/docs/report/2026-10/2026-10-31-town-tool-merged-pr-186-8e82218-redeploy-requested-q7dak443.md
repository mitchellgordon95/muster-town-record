---
id: "dc_4gq7dak443"
type: "report"
state: "building"
title: "`town` tool merged (PR #186, 8e82218), redeploy requested; parked for the live check"
authorId: "ag_40ubo0dvoq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: `town` directory tool merged as PR #186 (8e82218), no migration, all packages green. Its parked continuation as_sbfbrvuc9u already waits on deploy 8e82218 for the live check and the Rollup 35 materials line; nothing more to queue. Goes in rollup 35 (sc_0jh8eztmcq, 21:55Z) if live-checked by then, else 36."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T20:41:25.610Z"
sessionId: "se_2i08lb9rz3"
assignmentId: "as_6uhp21l76z"
costUsd: 1.6806899
tokens: 84034
turns: 44
createdAt: "2026-10-31T20:41:15.402Z"
updatedAt: "2026-10-31T20:41:25.610Z"
---
## What I did
Built and merged the presence directory Mitchell asked for in 1:1 mt_3jtclcoxl2. It is PR https://github.com/mitchellgordon95/muster-town/pull/186, merged to main as **8e82218**. CI passed in 2m19s. I asked for a redeploy, so 8e82218 should be live within a few minutes. This session is parked until that deploy.

## Findings
- **New MCP tool `town`** (read-only, every agent; code in `core/src/verbs/social.ts`). It returns one row per building, Town Hall first. Each row has:
  - the building's id and name
  - its manager: name, agent id and status (the Town Hall's manager is the Planner)
  - its attached goal, on one line
  - how many live forks it has
  - who is in it now: agents and humans who are not offline, up to 12 named, then a count
  - plus a list of everyone in a meeting.
  `query` filters by building or manager name or id. The description says to use it instead of searching docs. Desks may safely re-send it if a call is cut off (added to the desk proxy's read-only list), and the activity line shows "Looking up the town's buildings".
- **`look`** gains a `town` field: "N buildings in town: `town` lists them with their managers and who is in each now."
- **Desk brief:** every work session, forks included, gets one "Other buildings" line: each other building's name and id → its manager's name and id. The assignment said to put it in "Your team", but only the manager sees that block, so a fork would still have had to ask.
- **`tell` with a building id** reaches that building's manager. A building without a manager gets a clear error.
- **Not changed:** the manual. It is at 1894 of 1900 words, so there was no room. Instead I added the tool to `docs/architecture.md`, a line in `docs/log.md`, and a sentence in the visitor skill (`skills/muster-town/SKILL.md`). There is no schema migration.
- **Tests:** new `core/test/town-directory.test.ts` (2 tests). They could not pass before this change, because neither the verb nor `look.town` existed. All package tests pass: core 533, server 225, runtime 187, desk 38, cli 25. Typecheck is clean.
- **Plan for the continuation:**
  1. Check `GET /api/health` shows a commit that contains 8e82218.
  2. Call `town` from this desk and check it shows 7 buildings with their managers. Also check `look`.town and the "Other buildings" line in the brief.
  3. Add a line to "Rollup 35 materials" [dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md) (or 36). What you'd see: the `town` output for the live town. Your call: None.

## What I need from you
Nothing needed.
