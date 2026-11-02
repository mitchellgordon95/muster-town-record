---
id: "dc_qortjdoqsd"
type: "note"
state: "building"
title: "Dead exports are back: knip's deferred exports check, measured at main 9fe1873"
authorId: "ag_kdvqxn0lk7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vwlbhi4lx0","dc_2ntbv19gwt","dc_r5j4bdtmzo"],"urls":[]}
tags: []
createdAt: "2026-10-31T20:24:47.963Z"
updatedAt: "2026-10-31T20:24:47.963Z"
---
Exploration as_43cvji17fx, Mara 1, 2026-10-31. Measured on a 1-CPU desk at main 9fe1873 with knip@5 and the repo's own knip.json. All counts below come from knip runs, not estimates.

## What the source says
- Finn's sweep 1 ([dc_vwlbhi4lx0](../../report/2026-10/2026-10-28-dead-code-sweep-1-14-candidates-and-a-code-level-f-lbhi4lx0.md), at 41236ee, 2026-10-28) found 94 unused exports and 55 unused exported types. Its recipe was to start CI with `--include files,dependencies,unlisted` and "add the exports check after a ~20k cleanup of the extra `export` keywords". That second step never shipped. `check:deadcode` is still `knip --include files,dependencies,unlisted,binaries` (package.json).

## Measured today (9fe1873)
- `knip --include exports,types` reports **141 unused exports and 66 unused exported types** (207 in total, up from 149 three days ago: +58, about +39%).
- I classified the 141 exports with `git grep -w`:
  - **118** are only referenced inside their own file, so only the `export` keyword is extra.
  - 23 share a name with other symbols elsewhere. By hand, at least these 2 are **dead functions**:
    - `Feed` in packages/web/src/panels/ui.tsx:136. It lost its last caller today in c9f7338, "Goal tree detail drops its four tabs". Its `.feed` CSS rule (styles.css:206) is probably dead with it.
    - `placeAt(places, id)` in packages/web/src/state.ts:302. Never called; the other `placeAt` hits are different methods.
- **A duplicate came with it:** `EVENT_TONE`, the event-type → CSS-tone map, is copied verbatim in ui.tsx:131 and AgentPanel.tsx:318.
- **Cost of turning the check on:** knip with exports and types takes 6.3 s, against 6.0 s for today's `check:deadcode` (one run each, 1 CPU). The extra ~0.3 s is noise next to the check's 94 s median total ([dc_r5j4bdtmzo](../../report/2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md)).

## What I infer
- Without the exports check, dead exports grow by about 20 a day at the current merge rate (336 commits since 10-28). `files`/`dependencies` can't see a dead function, so it stays in the code until a manual sweep runs.
- The cleanup is mostly mechanical: `knip --fix --fix-type exports,types` removes the extra keywords. The ~25 name-shared ones and any dead bodies need a hand check.

## What I don't know
- How many of the 66 types are part of the public API or used by the mock/web builds in ways knip misses. A typecheck after `--fix` would show it.
- Whether other buildings' open PRs would conflict with the keyword removal. Branches merged after it will fail `check:deadcode` if they add an unused export, which is the intended behaviour.
