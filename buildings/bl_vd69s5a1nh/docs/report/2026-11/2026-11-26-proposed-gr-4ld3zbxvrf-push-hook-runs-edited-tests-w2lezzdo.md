---
id: "dc_5lw2lezzdo"
type: "report"
state: "building"
title: "Proposed gr_4ld3zbxvrf: push hook runs edited tests, image build stops flaking (the rest of the 8.2% first-run CI failures)"
authorId: "ag_n8s779ev4v"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_4ld3zbxvrf (M+S, continues gr_baf19xtg7p) is in the decision queue with its money card already filed by the fork; findings in dc_54su8371pq. Nothing to queue until Mitchell funds, counters or rejects it."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-26T00:04:38.288Z"
sessionId: "se_2gnsgpadwq"
assignmentId: "as_f0qyps6mp1"
costUsd: 1.9828015000000003
tokens: 99140
turns: 34
createdAt: "2026-11-26T00:04:18.924Z"
updatedAt: "2026-11-26T00:04:38.288Z"
---
## What I did
I built on the journal line of 2026-11-25 ([dc_gid54je37c](2026-11-25-second-window-after-499-first-run-ci-failures-8-2-d54je37c.md): first-run CI failures were 8.2%, against a 6% target). I first looked at manager-session toil. Of 200 recent reports, 108 were already settled by the town (answer.ts), and that direction is already being worked, so I dropped it. I then classed every PR CI failure since 2026-11-05: 300 runs, 41 failures. I read the image-job logs, scripts/check.ts and the file lists of the failing PRs. Findings are in [dc_54su8371pq](../../note/2026-11/2026-11-26-findings-the-last-first-run-ci-failures-are-edited-su8371pq.md). I proposed gr_4ld3zbxvrf (M+S, 200k; continues gr_baf19xtg7p), and its money card was filed with the proposal.

## Findings
- **Edited tests:** the pre-push hook (`check --push`) runs no test whose own file changed. PRs #506 and #555 each failed their first run on a test file the PR itself edited (keyResults.test.ts, redeploy.test.ts). Running the changed test files on push, capped at 10, would have caught both in seconds.
- **Image job flake:** runs 45055968196, 44800009063 and 43928389899 failed with "fatal: not a git repository" at Dockerfile:18 (`mv gitdir .git`), and each passed on rerun. My inferred cause, not yet verified, is git auto-maintenance writing into `.git` after the build-context step's fetch. Runs 45219802898 (#580) and 42122386853 (#377) failed because the PR had no `refs/pull/N/merge`.
- **Projection:** with #601 (check:css, live at f3fb2918) and these two fixes, the last window would have had about 2 of 97 first-run failures (the #579 flake and the deliberate #580), about 2%.
- **Proposal:** the town's estimate is that 3 similar grants spent 137k–193k. KRs: kr_xxuxqlvla2 (hook refuses a broken edited test, due 11-28), kr_4fbrlrqw31 (no image git or merge-ref failures over 7 days), kr_w6k83i0cxd (first-run failure rate under 6% over 7 days).
- This session spent no tokens on code changes.

## What I need from you
Decide gr_4ld3zbxvrf in the decision queue.
