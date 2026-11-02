---
id: "dc_o8pj741a8s"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Mara — notes"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T20:37:49.619Z"
updatedAt: "2026-10-31T20:37:49.619Z"
---
# 1:1: Mitchell and Mara

Kind: one-on-one. Facilitator: Mara. Attendees: Mara. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about your report "New key result kr_ealc55cjf5: dead exports are growing again (149 → 207 in 3 days); proposal gr_83jxsu8u0o is in your i…" ([dc_9ytzwe2me9](../../report/2026-10/2026-10-31-new-key-result-kr-ealc55cjf5-dead-exports-are-grow-tzwe2me9.md)). (presented: [New key result kr_ealc55cjf5: dead exports are growing again (149 → 207 in 3 days); proposal gr_83jxsu8u0o is in your in-tray. Nothing shipped.](../../report/2026-10/2026-10-31-new-key-result-kr-ealc55cjf5-dead-exports-are-grow-tzwe2me9.md))
- **Mara:** Hi Mitchell. Short version of that report: Finn's 10-28 dead-code sweep left knip's exports and types checks out of check:deadcode, so unused exports have crept from 149 to 207 in three days (141 exports + 66 types at 9fe1873). Two are really dead code (web `Feed` in panels/ui.tsx and `placeAt` in state.ts); most of the rest just need the `export` keyword dropped. I wrote kr_ealc55cjf5 for it and proposed gr_83jxsu8u0o (70k): one PR that removes the 207, turns the checks on in check:deadcode, so CI fails on the next one. The checks add about 0.3 s. The one thing to know before funding: the keyword removals touch other buildings' files, so funding is also the permission for that. Nothing else shipped since the last rollup. What would you like to discuss?
- **Mitchell:** sorry what is a dead export? and what does the check do?
- **Mara:** A dead export is a function, type or constant that a file marks `export` (so other files could import it) but nothing in the repo actually imports. Two flavours: (1) the thing is still used inside its own file, so only the `export` word is pointless, which is 118 of the 207; (2) nothing uses it anywhere, so it's truly dead code, like web `Feed` and `placeAt`. Why it matters: exports look like public API, so people keep them "just in case", they keep compiling and getting refactored, and dead ones hide among them.

The check: knip is the tool already behind `npm run check:deadcode` in CI. Today it only flags unused files and dependencies. Turning on its `exports` and `types` modes makes it also list every export nothing imports, and fail the check naming the file and symbol. So once we get the count to 0, a PR that leaves a new unused export behind goes red in CI with a line like `packages/web/src/panels/ui.tsx: Feed`. Cost is about 0.3 s per run.
- **Mitchell:** ok sgtm
- **Mara:** Great. Then the next step is just funding gr_83jxsu8u0o from your in-tray when you get to it; once it's funded I'll do the one PR and redeploy. Nothing else from me.

## Decisions

(none)
