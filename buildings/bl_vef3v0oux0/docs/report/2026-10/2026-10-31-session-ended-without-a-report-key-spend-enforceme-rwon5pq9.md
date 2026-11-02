---
id: "dc_36rwon5pq9"
type: "report"
state: "building"
title: "Session ended without a report: Key spend enforcement (b)+(c): debit as the session runs and count every token of a session that fails, crashes, is killed or ends without a report (Mitchell, 1:1 mt_x4"
authorId: "ag_j8w2j2zcfj"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "Key spend enforcement (b)+(c), second attempt (Mitchell, 1:1 mt_x40qq8poc3 decision 2; notes dc_bahpfdn1qw). The first run (as_l6dpiwsxzc, session se_3ojtmvjcwr, 58 turns, 182k adj. tokens) ended without a report while \"waiting on a check\": it ended its turn to wait for a background check and the session died. Rules for this run: never wait on a background task; run `npm run check` (or the targeted test files) in the foreground; commit and push to a branch early and often; if you must wait for something, park with submit_report resumeWhen, never by ending the turn.\n\nStep 0, recover: `git fetch origin && git branch -r | grep -i nell` for any branch the first run pushed (names like agent/nell-1/key-spend-enforcement…); also `git log origin/main --oneline -5` for anything already merged after 6b162cd. Build on it if it exists; otherwise start from main.\n\nBuild (Bank code pre-approved by Mitchell in that 1:1; keep it additive, no data rewrite):\n(b) Debit as the session runs, not only at its end: book usage incrementally (per turn or per N tokens, e.g. every turn's usage delta or every ~20k adj. tokens) through the same charge path (runtime session.ts chargeUsage → core budget.ts charge/recordUsage/drawFromInput), so Budget.fundingFor's next pick sees the real remaining balance of the key/input. The session-end charge becomes the remainder (total − already booked), never a double debit; the usage log keeps one row per session or clearly marks partial rows so finance-spend sums are unchanged. Host sessions and desk sessions both.\n(c) No lost usage on failure: a session that fails, crashes, is killed (spend-limit death, cap, container death) or ends without submit_report still has every token it used counted and debited. Find every exit path in runtime (host runAgentSession, desk runDeskSession, the fallback-report path) and make the final charge run in a finally/ensure step from the last known usage counters (the desk should report usage progressively, e.g. in heartbeats, so the host has the counters even if the desk dies). Tests: a test per exit path that the debit equals the usage; a test that incremental + final never exceeds total usage; existing check:finance identities stay green (npm run check:finance against the live API if reachable).\n\nDocs: add the rule to docs/invariants/bank.md (next free invariant number) and a line to the Bank topic pages you touch (rewrite dc_1l4r6tw7vl and dc_32xbgegtvn for what changed). Then PR + self-merge with green CI (or push straight to main with green tests), note the commit; CI redeploys. Report: the commit, what a human can check live (e.g. GET /api/sessions?limit=5 showing costUsd/tokens on a session that ended without a report; a Bank input balance moving mid-session), and anything not done. Do NOT do (a) (the Donate-form ceiling line): it is as_wwz0uvipwd, already queued separately."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T00:19:14.816Z"
sessionId: "se_3ojtmvjcwr"
assignmentId: "as_l6dpiwsxzc"
costUsd: 3.6544903999999994
tokens: 182725
turns: 58
createdAt: "2026-10-31T00:18:28.372Z"
updatedAt: "2026-10-31T00:19:14.816Z"
---
## What I did
Assignment: Key spend enforcement (b)+(c): debit as the session runs and count every token of a session that fails, crashes, is killed or ends without a report (Mitchell, 1:1 mt_x40qq8poc3 decision 2). The session ended without `submit_report`; this is a fallback report written by the runtime.

## Findings
I'll be notified when the check finishes; waiting on it before committing.

## What I need from you
Nothing needed.

