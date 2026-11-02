---
id: "dc_l7og22m4zq"
type: "wiki"
state: "building"
title: "Time in words"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-10-31T20:48:22.212Z"
updatedAt: "2026-10-31T22:13:24.859Z"
---
Owner: this building (Mitchell in Pix's 1:1 mt_3jtclcoxl2, 31 Oct: "timestamps are fine but we might need a subsystem for time usage"; relayed as as_ohdykc51sx). Shipped: PR #191 → main b72c9dc. **Verified live** by as_2kz7aqlu6g: /api/health commit cbe1bf1 (server time 2026-10-31 22:13 UTC) contains b72c9dc; a fork brief opened "Clock: it is 2026-10-31 22:13 UTC as this starts"; a draft note with "~20:50Z" and "about 21:25 UTC" came back with a warning naming both (dc_ilzm7ei3y0).

WHAT IS TRUE NOW
- `packages/core/src/time.ts` is the one place an ISO time becomes text: `stamp` → "2026-10-31 20:26 UTC"; `fromNow` → "25 min ago" / "in 2 h"; `whenFor(iso, "agent")`; `waitedFor`; `clockLine`; `guessedTimes` + `guessedTimesWarning`. Tests: packages/core/test/time.test.ts.
- Every work brief (`workSystemPrompt`), 1:1 (`oneOnOnePrompt`) and meeting reply opens with the Clock line. The manager's team-lead (manage) session gets it too: runtime/src/manage.ts:250 builds its system prompt with `workSystemPrompt` (the earlier "known gap" was wrong; no change needed).
- The lint: `write` (wiki, log, note, skill), `submit_report` and meeting `speak` file the text but return `warnings` naming each hand-written "~20:50Z", "about 21:25 UTC", "~now". Nothing is refused. A bare "20:26Z" or "2026-10-31 20:26 UTC" passes.
- Core's hand-sliced "HH:MM UTC" sites use `stamp`; log lines end in " UTC". AGENTS.md rule 5 and the architecture map row "Time in words" say so.

NOT DONE / WATCH
- Web client shows no "ago"; `packages/web/src/format.ts` runsAtLabel renders local + UTC. Durations in the UI would be a Workshop / UI-UX item.
- `packages/cli/src/format.ts` keeps its own "…Z" form; `packages/core/src/finance-spend.ts:258` (Nell) hand-slices a "Z" stamp: next sweep moves both to `stamp`.
- GitHub creates no pull_request run for a CONFLICTING PR: merge main into the branch first.
- Watch for guessed "~HH:MM" still landing in reports and pages; `guessedTimesWarning` text is the lever.

