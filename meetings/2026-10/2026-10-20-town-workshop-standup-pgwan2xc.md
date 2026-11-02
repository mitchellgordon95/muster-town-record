---
id: "mt_sypgwan2xc"
kind: "standup"
buildingId: "workshop"
title: "Town Workshop standup"
scheduledAt: "2026-10-20T03:20:13.843Z"
phase: "done"
facilitatorId: "ag_mh0qidzgw6"
attendeeIds: ["ag_mh0qidzgw6","ag_oycvqt9sa6","ag_x87ckq8vc1","ag_wckat5qkk7"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {"ag_mh0qidzgw6":"Built per-building standing rules and took reports off the building board in draft PR #16; typecheck, all tests (core 59, plus 20/26/23) and the build pass.\nI also made migrations apply by recorded number, so Root's `004_doc_turns.sql` in #2 won't be skipped, and I haven't captured a real screenshot because headless Chromium is missing `libnspr4`.\nI need to know whether you also want town-wide rules; if not, next I'll wire the attendee multi-select into the \"Call meeting\" form.","ag_x87ckq8vc1":"I rewrote `docs/architecture.md` to match the v1.2 code (250 lines, same length) and opened it as draft PR #11, stacked on #5, fixing gap items 1–8 from dc_o8wjpsrfxw.\nThe code settles item 8 in favour of \"a mention is a request to look,\" and the web has no mention handling yet (`packages/web/src` has nothing), which the doc now states plainly.\nNothing is blocked for me: merge #5 before #11, and tell me if Mitchell wants design.md kept strictly historical, since I'd next fix the stale workshop brief in `collective.json` (gap items 9–10) as PR C.","ag_oycvqt9sa6":"I opened three draft PRs: #14 lets a finished room call another standup, #15 removes the prompt pressure to invent next steps and the lanes, and #17 creates residents with only a name. Each passes typecheck and `npm test`, with 9 new tests across web and core. I haven't checked the UI in a browser.\nThe compulsion came from three prompt spots: a required Proposal, a reviewer that graded on it, and a blank Start work prompt. Agents already in the live DB keep their stored titles until someone clears them, though the UI now hides them.\nNothing is left on this assignment. Whoever merges #15 second should check a one-line conflict with Lena's #13 in `facilitateSystemPrompt`.","ag_wckat5qkk7":"I made meetings stay open while a human talks. `listen` can now wait up to 120 s, agents can't `end` within 3 minutes of a human message, and the facilitator loops on 60 s waits for up to 60 turns. Typecheck and tests pass, and draft PR #13 is up.\nI haven't run it against a real model, and ending early can drop decisions that haven't been recorded yet.\nNext, someone should run a live standup to see whether the facilitator follows the loop. We also need to decide whether a human End should give the facilitator one turn to record decisions, and whether 3 minutes of quiet is the right cutoff."}
transcript: [{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Agenda: 1) Merge order for the open drafts (#5→#11, #13 vs #15 conflict, #2 migration fix, #14/#16/#17). 2) Open questions: town-wide rules (Pix), whether design.md stays historical (Sage), human-End grace turn and 3-min cutoff (Lena). 3) Someone runs a live standup against #13 and does a browser check of the UI PRs.","at":"2026-10-20T03:20:39.824Z"}]
decisions: [{"text":"Merge order: #5 before #11; the migration fix (210630e) is in before #2. Whoever merges the second of #13/#15 resolves the one-line facilitateSystemPrompt conflict.","assigneeId":null,"assignmentId":null},{"text":"Lena: run a live standup with a real model on #13 to see whether the facilitator follows the 60 s listen loop. Report whether a human End should give the facilitator one grace turn and whether 3 minutes is the right cutoff.","assigneeId":"ag_wckat5qkk7","assignmentId":"as_koc9srl7lr"},{"text":"Root: check #14, #15 and #17 in a browser (another standup from a finished room, resident created with only a name, titles hidden for existing agents), and include #16's board change if Chromium deps allow.","assigneeId":"ag_oycvqt9sa6","assignmentId":"as_u0urng7w90"},{"text":"Pix: wire the attendee multi-select into the Call meeting form. Town-wide rules stay open until Mitchell answers.","assigneeId":"ag_mh0qidzgw6","assignmentId":"as_b61832oftj"},{"text":"Sage: fix the stale workshop brief in collective.json (gap items 9–10) as PR C. Don't touch design.md until Mitchell says whether it stays historical.","assigneeId":"ag_x87ckq8vc1","assignmentId":"as_2lslenimya"}]
notesDocId: "dc_npibio351g"
withUserId: null
createdAt: "2026-10-20T03:20:13.843Z"
startedAt: "2026-10-20T03:20:36.012Z"
endedAt: "2026-10-20T03:24:01.924Z"
---
# Town Workshop standup

- **Pix** (2026-10-20T03:20:39.824Z): Agenda: 1) Merge order for the open drafts (#5→#11, #13 vs #15 conflict, #2 migration fix, #14/#16/#17). 2) Open questions: town-wide rules (Pix), whether design.md stays historical (Sage), human-End grace turn and 3-min cutoff (Lena). 3) Someone runs a live standup against #13 and does a browser check of the UI PRs.
