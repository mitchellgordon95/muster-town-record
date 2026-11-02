---
id: "dc_voahxk4og1"
type: "report"
state: "building"
title: "Time usage is now a core subsystem (PR #191 → b72c9dc): briefs and 1:1s open with the server clock, agents are told to stamp only server-read times, and a guessed \"~HH:MM UTC\" in a page, report or meeting line comes back with a warning"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_l7og22m4zq"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/191"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Its parked continuation as_e8kwwso7fj already exists (verify b72c9dc live, roll up); live is 36a8a86 which contains b72c9dc. This team-lead session rolls PR #191 up now; the verification is queued as its own small assignment instead of a second rollup."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-31T21:01:40.820Z"
sessionId: "se_b02ah5qn8z"
assignmentId: "as_ohdykc51sx"
costUsd: 8.061732249999999
tokens: 161235
turns: 83
createdAt: "2026-10-31T21:00:22.827Z"
updatedAt: "2026-10-31T21:01:40.820Z"
---
## What I did
Directed by Mitchell in Pix's 1:1 mt_3jtclcoxl2 (relayed by Pix). Built, tested, merged and queued a redeploy for one PR: https://github.com/mitchellgordon95/muster-town/pull/191 (merge commit b72c9dc; CI green on the PR; `npm run check` green locally: docs, deadcode, typecheck, 1204 tests). Told Pix (queued to it as as_9ea5248h7y). Topic page "Time in words" [dc_l7og22m4zq](../../wiki/2026-10/2026-10-31-time-in-words-og22m4zq.md); my key-results page updated; log lines added.

## Findings
What the repo had: two "ago" helpers (core `relativeTime` "5m ago", the deck's `waitedFor` "4.1 h"), 15 hand-sliced `HH:MM UTC` sites across core (schedules, wakes, waits, presence, forks, caps, memory, prompts), and no clock at all in any brief: an agent's only stamps were event times and "updated 1m ago", so it narrated the clock from guesses (Pix's pages ran 45–70 min ahead).

What shipped (Pix's suggested shape, kept):
- **`packages/core/src/time.ts`**, the one place a time becomes text: `stamp` ("2026-10-31 20:26 UTC", the server-read form agents and event texts write), `fromNow` ("25 min ago" / "in 2 h", what a human reads; replaces "5m ago"), `whenFor(iso, "agent")` (stamp with the duration beside it), `waitedFor` (moved from the deck), `clockLine`, `guessedTimes`. All 15 hand-sliced sites now call `stamp`; log lines end in " UTC". Tests in `packages/core/test/time.test.ts` (9).
- **The clock in every brief:** work briefs, 1:1s and meeting replies open with "Clock: it is <server stamp> as this starts" and the rule (you have no clock; write only times read from the server: event ts, doc updatedAt, /api/health, `date` on the desk; durations for humans, never a guessed "~HH:MM UTC"). 1:1 transcript lines and each streamed human line carry their stamp, so "what time is it" has an honest answer.
- **The lint:** `write` (wiki, log, note, skill), `submit_report` and meeting `speak` file the text as before but return a `warnings` line naming each hand-written "~20:50Z", "about 21:25 UTC" or "~now". Nothing is refused. (My own wiki page carried a "~20:50Z"; fixed.)
- Docs: architecture map row "Time in words", AGENTS.md standing rule 5, docs/log.md.

Left out, on purpose: the web UI (no "ago" anywhere; `runsAtLabel` shows local + UTC) is the Workshop's / UI-UX's if Mitchell wants durations on screen; the CLI keeps its own stamp form; one new hand-sliced stamp in Nell's `finance-spend.ts` landed after I branched (her building).

Toil found on the way: GitHub creates no pull_request run at all for a CONFLICTING PR (not even queued), which looked like a CI outage; main moved 4 times during this session, so the PR needed main merged in twice (log.md conflicts both times) before a run existed. Pix's new `{pr: N}` wait (#190) merged alongside.

## What I need from you
Nothing needed. Live should be b72c9dc (redeploy called, not waited for); the parked continuation verifies it and rolls it up.
