---
id: "mt_lsyqj98z0w"
kind: "one-on-one"
buildingId: "bl_vd69s5a1nh"
title: "1:1: Mitchell and Mara"
scheduledAt: "2026-11-08T03:15:10.810Z"
phase: "discussing"
facilitatorId: "ag_croreod6q3"
attendeeIds: ["ag_croreod6q3"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"us_1la74k332n","speakerKind":"user","text":"I'd like to talk about your report \"Work routing map filed for Mitchell's meeting (dc_4xww7x920l): 21 paths create work, 13 can land on a forking manager's…\" (dc_9gcxz43hbc).","at":"2026-11-08T03:15:10.813Z","attachment":{"kind":"doc","ref":"dc_9gcxz43hbc","title":"Work routing map filed for Mitchell's meeting (dc_4xww7x920l): 21 paths create work, 13 can land on a forking manager's own queue; Workshop PR #369 closes 3","excerpt":"Live: 565a075 (nothing of ours in it; this rollup carries the map Mitchell asked for via Pix, mtpeubjyoo0k). Shipped 1. The work-routing map you asked for is filed What it is: A read-only map of every path that creates work in the town (21 of them, each with file:line and the test that names it), which queue it lands on, what gates it, and how it comes back. 13 paths can put work on a forking man…"}},{"speakerId":"ag_croreod6q3","speakerKind":"agent","text":"Hi Mitchell. I've reread the rollup and the map behind it (dc_4xww7x920l). The short version: 21 code paths create work; 13 of them can drop a job on a forking manager's own queue, which means the manager runs it and the building's in-tray waits (runtime/src/manage.ts:167). Since then the Workshop's PR #369 has landed on main (decisionQueue is in domain.ts:337, used at domain.ts:214 and meetings.ts:565), so 3 of those 13 are closed: meeting decisions naming the manager, the auto-approve of the manager's reports, and review continue/redirect on a manager's own report. 10 remain: tell relays to a building id, @mentions, outbox answers, amended-decision wakes, a human's assign/REST work naming the manager, schedule takerId, retry, flags naming the manager, and a manager parking its own work. The one decision I'd like from you today is §4 question 1: fix those 10 one PR at a time (Workshop-style, like #369), or make createAssignment default to the building queue whenever the named agent is a forking manager, with an explicit manager-only flag for the two jobs that must stay (checkpoint, grant funded/countered/rejected)? My recommendation is the one rule: it's one change in domain.ts:59-62 plus a flag on grants.ts:785 and :817, and the docs fixes (architecture.md diagram, invariants 7–8, how-work-gets-done §6) can then describe one rule instead of 21 cases. Which way do you want it, and whose PR: ours or the Workshop's?","at":"2026-11-08T03:15:33.724Z"}]
decisions: []
notesDocId: null
withUserId: "us_1la74k332n"
createdAt: "2026-11-08T03:15:10.810Z"
startedAt: "2026-11-08T03:15:10.810Z"
endedAt: null
---
# 1:1: Mitchell and Mara

- **Mitchell** (2026-11-08T03:15:10.813Z): I'd like to talk about your report "Work routing map filed for Mitchell's meeting (dc_4xww7x920l): 21 paths create work, 13 can land on a forking manager's…" (dc_9gcxz43hbc).
- **Mara** (2026-11-08T03:15:33.724Z): Hi Mitchell. I've reread the rollup and the map behind it (dc_4xww7x920l). The short version: 21 code paths create work; 13 of them can drop a job on a forking manager's own queue, which means the manager runs it and the building's in-tray waits (runtime/src/manage.ts:167). Since then the Workshop's PR #369 has landed on main (decisionQueue is in domain.ts:337, used at domain.ts:214 and meetings.ts:565), so 3 of those 13 are closed: meeting decisions naming the manager, the auto-approve of the manager's reports, and review continue/redirect on a manager's own report. 10 remain: tell relays to a building id, @mentions, outbox answers, amended-decision wakes, a human's assign/REST work naming the manager, schedule takerId, retry, flags naming the manager, and a manager parking its own work. The one decision I'd like from you today is §4 question 1: fix those 10 one PR at a time (Workshop-style, like #369), or make createAssignment default to the building queue whenever the named agent is a forking manager, with an explicit manager-only flag for the two jobs that must stay (checkpoint, grant funded/countered/rejected)? My recommendation is the one rule: it's one change in domain.ts:59-62 plus a flag on grants.ts:785 and :817, and the docs fixes (architecture.md diagram, invariants 7–8, how-work-gets-done §6) can then describe one rule instead of 21 cases. Which way do you want it, and whose PR: ours or the Workshop's?
