---
id: "dc_z8mnleg08h"
type: "report"
state: "building"
title: "gr_8i952perny step 1: Grants.stop in draft PR #275 (CI pending)"
authorId: "ag_5wllewpmtw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of gr_8i952perny in draft PR #275; your parked continuation merges and redeploys it. Step 2 (web Stop grant button, stopping label, in-tray row, deck slide, live stop with Bank check) queued separately, starting when PR #275's CI finishes."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T02:58:39.803Z"
sessionId: "se_0nm489w0x5"
assignmentId: "as_nn00bsaeza"
costUsd: 3.5753478
tokens: 178767
turns: 64
createdAt: "2026-11-03T02:58:24.904Z"
updatedAt: "2026-11-03T02:58:39.803Z"
---
## What I did
Built step 1 of gr_8i952perny: the core verb, the server route and tests. Everything is in one draft PR: https://github.com/mitchellgordon95/muster-town/pull/275 (commits 95e89f3 and 29da768, branched off main 335c586). Before pushing I ran these at my desk, all green: typecheck, core 683/683, server 264/264, runtime forks 12/12, check:docs and knip. CI is still running. I added item 21 to the rollup candidates page [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md); it is API-only for now. I'm parking on {pr: 275}.

## Findings
**What the PR does**
- `POST /api/grants/:id/stop {reason}` calls core `Grants.stop`.
- Who can stop: a human with `building.fund`, or the captain of the grant's goal. A manager gets 403. The reason is required (400 if blank). A proposed grant gets 409: withdraw or reject it instead.
- The grant first goes to a new status, `stopping` (schema only; status is a TEXT column, so no migration). It is not live: no new work can be charged to it (lanes.ts now refuses it), and free-tokens.ts stops counting its claim straight away.
- Every fork running a session on the grant is interrupted. This uses `interruptFork`, the no-permission half I split out of `requestForkStop`, with the reason and the existing 5-min hard stop.
- Queued grant work is cancelled, and each row's `heldReason` reads "Grant stopped: <reason>". No held rows are left.
- Open key results are archived as missed, with the note "Grant stopped: <reason>". No postmortem is queued: the reason is the why.
- The manager gets a system message.
- The runtime tick runs `finishStopping`. Once no session is running on the grant it closes as `stopped`; if none was running at the stop, it closes at once. No runtime change was needed beyond that one tick line.
- The `grant.closed` event names the human who stopped it and carries {reason, spentTokens, grantTokens, unspentTokens, returnedTo: pool|input, fundedWith}.

**Two side changes**
- A funder's `close` with outcome stopped on a live grant now goes through `stop`.
- I fixed a stop_fork bug that was already there: the first stop in a town with no `pendingForkStops` marker counted its own request twice.

**Key results**
- **kr_ghexd88frr: claimable once merged.** The server test covers human stop (200), manager stop (403), manager close-stopped on a funded grant (403) and manager withdraw of a proposal (200).
- **kr_4s0ccmvtsp: claimable once merged.** The core test covers one running fork plus one queued assignment: the fork is interrupted, the queued one is cancelled with the reason, the grant stays `stopping` until the session ends, then closes as stopped.
- **kr_kaz3nj127k: core half done.** Tested:
  - Pool-funded: free tokens go up by granted minus spent.
  - Member-funded: the input balance is unchanged (460,000 before and after), and the event says the rest stays on the input.
  - Bank accounting is not touched beyond the existing claim rule.
  - Still open: "GET /api/bank agrees with the Bank page" needs a live check in step 2.
- **kr_f46tddd9as: core half done.** The server test checks that GET of the grant shows every key result missed with the note; the event and the manager's message are in place.

**What step 2 must still do**
- A web "Stop grant" button with a required reason, and a label for `stopping` in GrantRow and keyResults.ts (it currently has no label).
- A "stopped" row in the Town Hall in-tray and a review-deck slide.
- A live stop on a throwaway grant: check the Bank page's free tokens against GET /api/bank, and take a picture for rollup item 21.

## What I need from you
Nothing needed.
