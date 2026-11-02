---
id: "mt_k9qj4ygnmt"
kind: "one-on-one"
buildingId: "bl_vd69s5a1nh"
title: "1:1: Mitchell and Mara"
scheduledAt: "2026-10-31T20:35:57.738Z"
phase: "done"
facilitatorId: "ag_croreod6q3"
attendeeIds: ["ag_croreod6q3"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"us_1la74k332n","speakerKind":"user","text":"I'd like to talk about your report \"New key result kr_ealc55cjf5: dead exports are growing again (149 → 207 in 3 days); proposal gr_83jxsu8u0o is in your i…\" (dc_9ytzwe2me9).","at":"2026-10-31T20:35:57.740Z","attachment":{"kind":"doc","ref":"dc_9ytzwe2me9","title":"New key result kr_ealc55cjf5: dead exports are growing again (149 → 207 in 3 days); proposal gr_83jxsu8u0o is in your in-tray. Nothing shipped.","excerpt":"Live: e41f375 (Pix's 181 and Nell's 180; nothing from this building since 34b7e53). Shipped Nothing shipped from this building since the last rollup (dcjela5ondmt). This rollup exists because a key result was written. Decided - dcipcpcdwqog → approve. Mara 1 ran knip with exports and types at 9fe1873: 141 unused exports plus 66 unused types (207), up from 149 on 10-28. Two are dead functions (web…"}},{"speakerId":"ag_croreod6q3","speakerKind":"agent","text":"Hi Mitchell. Short version of that report: Finn's 10-28 dead-code sweep left knip's exports and types checks out of check:deadcode, so unused exports have crept from 149 to 207 in three days (141 exports + 66 types at 9fe1873). Two are really dead code (web `Feed` in panels/ui.tsx and `placeAt` in state.ts); most of the rest just need the `export` keyword dropped. I wrote kr_ealc55cjf5 for it and proposed gr_83jxsu8u0o (70k): one PR that removes the 207, turns the checks on in check:deadcode, so CI fails on the next one. The checks add about 0.3 s. The one thing to know before funding: the keyword removals touch other buildings' files, so funding is also the permission for that. Nothing else shipped since the last rollup. What would you like to discuss?","at":"2026-10-31T20:36:06.316Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"sorry what is a dead export? and what does the check do?","at":"2026-10-31T20:36:44.736Z"},{"speakerId":"ag_croreod6q3","speakerKind":"agent","text":"A dead export is a function, type or constant that a file marks `export` (so other files could import it) but nothing in the repo actually imports. Two flavours: (1) the thing is still used inside its own file, so only the `export` word is pointless, which is 118 of the 207; (2) nothing uses it anywhere, so it's truly dead code, like web `Feed` and `placeAt`. Why it matters: exports look like public API, so people keep them \"just in case\", they keep compiling and getting refactored, and dead ones hide among them.\n\nThe check: knip is the tool already behind `npm run check:deadcode` in CI. Today it only flags unused files and dependencies. Turning on its `exports` and `types` modes makes it also list every export nothing imports, and fail the check naming the file and symbol. So once we get the count to 0, a PR that leaves a new unused export behind goes red in CI with a line like `packages/web/src/panels/ui.tsx: Feed`. Cost is about 0.3 s per run.","at":"2026-10-31T20:36:51.602Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"ok sgtm","at":"2026-10-31T20:37:26.686Z"},{"speakerId":"ag_croreod6q3","speakerKind":"agent","text":"Great. Then the next step is just funding gr_83jxsu8u0o from your in-tray when you get to it; once it's funded I'll do the one PR and redeploy. Nothing else from me.","at":"2026-10-31T20:37:29.232Z"}]
decisions: []
notesDocId: "dc_o8pj741a8s"
withUserId: "us_1la74k332n"
createdAt: "2026-10-31T20:35:57.738Z"
startedAt: "2026-10-31T20:35:57.738Z"
endedAt: "2026-10-31T20:37:49.621Z"
---
# 1:1: Mitchell and Mara

- **Mitchell** (2026-10-31T20:35:57.740Z): I'd like to talk about your report "New key result kr_ealc55cjf5: dead exports are growing again (149 → 207 in 3 days); proposal gr_83jxsu8u0o is in your i…" (dc_9ytzwe2me9).
- **Mara** (2026-10-31T20:36:06.316Z): Hi Mitchell. Short version of that report: Finn's 10-28 dead-code sweep left knip's exports and types checks out of check:deadcode, so unused exports have crept from 149 to 207 in three days (141 exports + 66 types at 9fe1873). Two are really dead code (web `Feed` in panels/ui.tsx and `placeAt` in state.ts); most of the rest just need the `export` keyword dropped. I wrote kr_ealc55cjf5 for it and proposed gr_83jxsu8u0o (70k): one PR that removes the 207, turns the checks on in check:deadcode, so CI fails on the next one. The checks add about 0.3 s. The one thing to know before funding: the keyword removals touch other buildings' files, so funding is also the permission for that. Nothing else shipped since the last rollup. What would you like to discuss?
- **Mitchell** (2026-10-31T20:36:44.736Z): sorry what is a dead export? and what does the check do?
- **Mara** (2026-10-31T20:36:51.602Z): A dead export is a function, type or constant that a file marks `export` (so other files could import it) but nothing in the repo actually imports. Two flavours: (1) the thing is still used inside its own file, so only the `export` word is pointless, which is 118 of the 207; (2) nothing uses it anywhere, so it's truly dead code, like web `Feed` and `placeAt`. Why it matters: exports look like public API, so people keep them "just in case", they keep compiling and getting refactored, and dead ones hide among them.

The check: knip is the tool already behind `npm run check:deadcode` in CI. Today it only flags unused files and dependencies. Turning on its `exports` and `types` modes makes it also list every export nothing imports, and fail the check naming the file and symbol. So once we get the count to 0, a PR that leaves a new unused export behind goes red in CI with a line like `packages/web/src/panels/ui.tsx: Feed`. Cost is about 0.3 s per run.
- **Mitchell** (2026-10-31T20:37:26.686Z): ok sgtm
- **Mara** (2026-10-31T20:37:29.232Z): Great. Then the next step is just funding gr_83jxsu8u0o from your in-tray when you get to it; once it's funded I'll do the one PR and redeploy. Nothing else from me.
