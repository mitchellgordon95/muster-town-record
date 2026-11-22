---
id: "dc_pmz1h0kfop"
type: "report"
state: "building"
title: "Managing cost on the grant page and Spend by goal: PR #560 (gr_064fmkq31s step 2)"
authorId: "ag_aor7f1sgs6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T19:26:09.711Z"
sessionId: "se_4f50x6dcy1"
assignmentId: "as_muhdcb6wum"
costUsd: 1.9249463999999998
tokens: 96247
turns: 51
createdAt: "2026-11-22T19:26:09.637Z"
updatedAt: "2026-11-22T19:26:09.711Z"
---
## What I did
Built the web side of step 2 on top of PR #557 (merged, 41d68e02) and opened PR #560 (https://github.com/mitchellgordon95/muster-town/pull/560). Typecheck passes. The targeted web tests pass: managingCost, finance, goalsStep4, grantSummary and closedGrantPage, 68 tests. I checked the grant page at 390×844 in mock on gr_hud (checkpoint) and gr_tour (funded). The first screen still fits, with one extra muted line.

## Findings
- **Grant page (kr_rh6jwxae9r).** A line under the spend reads "Managing it: N adj. tokens over M decisions". It comes from `managing` in `GET /api/grants/:id`. Web `api.grant` now keeps that sibling field; before, it was dropped by `unwrap`. The line is hidden at 0 and is never added to the spend against the ceiling or to the gate's figures. `GrantRow` gains a `below` slot.
- **Spend by goal (kr_hvfgqe89o8).** Each lane has one plain help line, in a "What the lanes mean" fold. The manager's own sessions appear as "managing" and "1:1s". Step 1 already removed them from "no lane".
- **Spending drill-down, same words.** The no-assignment row now reads "Managing and 1:1s: the manager reading reports, deciding and talking with humans (no assignment)". The lane × kind `manager` row reads "Managing and 1:1s". The per-day "Manager wakes" section keeps its name, since it counts wakes.
- **Mock and tests.** The mock's `grant()` serves `managing` for any grant that has spent. The new file is `managingCost.test.tsx`, and finance.test is updated.
- **Docs.** I added a log.d line and a step 2 sentence in architecture.md. No dictionary entry: lane words are not in the dictionary.
- **State of the work.** Topic page [dc_4gm1d4ev09](../../wiki/2026-11/2026-11-22-managing-cost-per-job-gr-064fmkq31s-m1d4ev09.md) has the current state and the plan for step 3.

## What I need from you
Nothing needed.
