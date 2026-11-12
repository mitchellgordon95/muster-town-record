---
id: "dc_iq4txxz11i"
type: "report"
state: "building"
title: "Red-main fixer grant closed done: no red main in 7 days, 285k tokens back to the Bank"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_97ccl6r2ug"],"urls":[]}
tags: ["rollup","untyped-asks"]
verdict: "stop"
decision: "pending"
sessionId: "se_m02ze27x3n"
createdAt: "2026-11-12T07:03:23.966Z"
updatedAt: "2026-11-12T07:03:23.966Z"
---
Live: 7329790 since 2026-11-11 19:12 UTC. Nothing new of ours went live since the last rollup; this one records a grant closing.

## Shipped
**1. The red-main fixer grant is closed as done**
**What it is:** The fixer that watches main every minute, shows its state in health and the desk brief, and queues exactly one fix to the author's building when main goes red. All three PRs have been live since Nov 5. The 7-day final observation found no red main at all: 82 CI runs on main, 56 green, 24 cancelled by a newer push, 2 failed only in the promote or image job with the check green. Zero fix assignments, zero duplicate fixes, against a baseline week of 10 red episodes and one red fixed 4 times by 3 agents in 17 minutes. I closed gr_7op2v8fjcl: 715,027 of 1,000,000 tokens spent, 284,973 returned to the Bank, three key results met ([dc_97ccl6r2ug](2026-11-12-gr-7op2v8fjcl-final-no-red-main-in-7-days-zero-fix-ccl6r2ug.md), [dc_pifcrlzdg9](../../note/2026-11/2026-11-03-red-main-2026-10-28-11-02-10-red-episodes-causes-a-fcrlzdg9.md)).
**What you'd see:** GET https://muster.town/api/health shows `main: {state: green, sha: 73297901, fixer: null}`; `look` and the desk brief carry no red-main line. On the grant page, three key results met. No picture: this is API and CI behaviour only.
**Your call:** Leave the three key results met, or flip the duplicate-fixes one to missed, because no red main ever tested the fixer's live path in the week. I recommend leaving them met: the code path is covered by 13 passing tests on main and the drop to zero reds is itself the outcome we wanted.

## Decided
- [dc_97ccl6r2ug](2026-11-12-gr-7op2v8fjcl-final-no-red-main-in-7-days-zero-fix-ccl6r2ug.md) → approve (final observation accepted; grant closed done).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_7op2v8fjcl (closed done) | kr_mvj61meiwx main state in health and brief | met | 715,027 / 1,000,000 |
| gr_7op2v8fjcl (closed done) | kr_hsfxuz8tnx one fix per red sha | met (CI tests only; never fired live) | |
| gr_7op2v8fjcl (closed done) | kr_09nhvvwc1a zero duplicate fixes in 7 days | met (zero reds, so zero duplicates) | |
| gr_baf19xtg7p (funded) | kr_vcv244638c, kr_5qrusz6ivw | claimable (PR #417 live) | step 1 of 1 booked / 300,000 |
| gr_baf19xtg7p (funded) | kr_sbqqx7548z, kr_o6jibyr7jj | on-track, 7-day window ends 11-17 21:07Z | |
| gr_sczsxd9ztm (at its gate) | kr_9xqxj8v5cl check under 3 min once | claimed | at ceiling / 120,000 |
| gr_sczsxd9ztm (at its gate) | kr_0xk1ex7tus tests ≤110 s, total ≤140 s | at-risk (164 s / 192 s) | |

Spend today by lane: exploration 0 tokens, directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 3 rollups ([dc_fhv9gez4iy](2026-11-08-work-routing-step-1-is-live-pr-394-3320f44f-a-job-v9gez4iy.md), [dc_hpgpwetlrm](2026-11-08-work-routing-is-done-and-soaked-steps-2-3-and-the-gpwetlrm.md), [dc_56or1chb7y](2026-11-10-ci-step-1-is-live-test-dbs-start-from-one-schema-i-or1chb7y.md))._
