---
id: "dc_92ekyyo5wo"
type: "report"
state: "building"
title: "Key results auto-met on close: PR #297 open, parked on CI"
authorId: "ag_4xjo9rsupv"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The parked continuation as_dg64263mu9 (waiting on PR #297 CI) carries the rest: merge main if needed, check migration 087 is still unique, merge if green, redeploy. Folds into rollup 44 as item 27 (migration 087 rewrites live data: 13 claimed key results go to met; \"Your call\" must say so)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T02:54:08.494Z"
sessionId: "se_bdgua1uy45"
assignmentId: "as_mygyiflb6n"
costUsd: 2.0966744000000004
tokens: 104834
turns: 43
createdAt: "2026-11-04T02:53:56.365Z"
updatedAt: "2026-11-04T02:54:08.494Z"
---
## What I did
I built town hall mt_v09cn7a8yr decision 2 ("auto met") and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/297 (branch agent/pix-1/key-results-auto-met-on-grant-close-no-h, one commit). The work is parked until its CI finishes. Then I merge main if needed, merge the PR if green and redeploy. I added item 27 to the Rollup materials page [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).

## Findings
- **Core** (`grants.ts closeDone`): when a grant closes as done, each open key result now goes straight to `met`. Its note is the close note, its "by" is the person or agent who closed it, and it is archived under its goal. The step uses an internal `closing` flag on `updateKeyResult`. A manager still cannot set met or missed through PATCH, and the "at most claimed" rule for `checkpoint_grant` is unchanged. The funders' notice now says the key results are marked met and that they can flip one to missed from the grant. Stopped grants are unchanged.
- **In-tray and deck**: `grantsAwaitingDecision` no longer includes closed-as-done grants, so the in-tray row and its badge count are gone. The review deck no longer has the "closed as done — mark" slide. The close rollup shows as an ordinary rollup.
- **Web**: `Places.tsx` drops the "Closed as done: mark the key result" section. On a closed-as-done grant, someone who can fund sees "Mark missed" (only once they type why, which queues a postmortem) and "Back to met". The mock (sim, server, fixture) was updated to match.
- **Text and docs**: I rewrote the `close_grant` and `checkpoint_grant` tool descriptions, the manager prompt lines, the `close_grant` verb note, docs/how-work-gets-done.md (§4 and the loop diagram), docs/goals.md, docs/goal-directed-budgets.md and docs/invariants/grants.md.
- **Migration 087** (unique on main as of 02:5xZ, where the highest is 086): it back-fills key results still `claimed` on grants already closed as done to `met` and archives them. **This rewrites live data.** The live in-tray had 13 such grants, including gr_rdzg83m0al, gr_ukrou4zjha and gr_cuobjlny6r. After the deploy they leave the Town Hall in-tray already marked met.
- **Tests**:
  - Core: 705/705 pass. The close test now checks met, archived and statusBy, that there is no in-tray row or deck slide, and that missed needs a why and can be undone. There is a new 087 back-fill test, and the stop tests still pass.
  - Server: grants.test.ts 4/4, including a new test of the close route plus in-tray, deck and PATCH flip.
  - Web: 297/297. Typecheck, check:docs and deadcode are clean.
- **Picture**: none. The change is in the API and the in-tray only: a section disappears.

## What I need from you
Nothing needed. A heads-up: once it deploys, the 13 grants waiting in the in-tray for met/missed are marked met automatically. If one did not ship, flip it to missed on its grant.
