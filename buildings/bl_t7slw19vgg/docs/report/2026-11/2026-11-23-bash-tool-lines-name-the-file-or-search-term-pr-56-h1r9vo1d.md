---
id: "dc_28h1r9vo1d"
type: "report"
state: "building"
title: "Bash tool lines name the file or search term: PR #563, parked to merge when green"
authorId: "ag_f0fb4l7h1f"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:17:07.921Z"
sessionId: "se_q3phhwtg8r"
assignmentId: "as_26fh4twyqh"
costUsd: 2.2739041000000006
tokens: 113695
turns: 43
createdAt: "2026-11-23T16:17:07.400Z"
updatedAt: "2026-11-23T16:17:07.921Z"
---
## What I did
Collected 2,937 real Bash calls from live /api/events (2026-11-19 15:18Z to 11-23 16:08Z). Rewrote `describeCommand` in packages/runtime/src/describe.ts so each line names the file or the search term. Fixed the "Now: Now" head line in packages/web/src/panels/nowLine.ts. Added scripts/tool-label-census.mjs. Typecheck, knip and check:docs pass. Runtime tests: 277 pass. Web tests: 478 pass. PR https://github.com/mitchellgordon95/muster-town/pull/563 is parked to merge when green.

## Findings
- **What the lines say now.** "Reading jobs.ts", "Searching for captainRequests, accessRequests", "Searching finance.ts for export function townFinance", "Editing home.css", "Writing go.mjs", "Running a Python script on GrantPanel.tsx", "Listing the migrations folder", "Taking a screenshot". When nothing safe is found, the old generic line stays.
- **What a line never shows.** A line shows only a file's own name or a cleaned search term. A term with `/`, `$`, NAME=value or a token shape falls back to the file name or to "Searching files". A new quote-aware splitter replaces the old naive split at `|` and `;`, which used to cut `grep "a\|b"` in two. Folders are also removed from the Bash descriptions agents write themselves.
- **Numbers.**
  - Corpus of 2,937 calls: 5.0% generic (old labels: about 60%), 0 leaks.
  - Census on the live window at 16:12Z: 131 of 371 live lines are generic (35.3%). This branch would label 15 of those 371 as generic (4.0%), with 0 leaks.
  - The test fixture packages/runtime/test/fixtures/bash-commands.json holds 160 real commands. It asserts each command's label, no leak and a generic share of 25% or less. I screened it for secrets: it contains only env-var names, no values.
- **What is still generic.** Most of it is greps for API routes (`/api/...`). These stay generic on purpose because of the no-slash rule.
- **Bash descriptions are lost.** Forks pass a Bash `description`, but it never reaches the events: only 28 of 2,937 calls had one. Desk `clipInput` does not strip it. Not needed for the key results.
- Topic page with the plan for step 2: [dc_20hbau9n0v](../../wiki/2026-11/2026-11-23-tool-call-lines-name-what-they-touch-gr-93s00hyq1l-hbau9n0v.md).

## What I need from you
Nothing needed.
