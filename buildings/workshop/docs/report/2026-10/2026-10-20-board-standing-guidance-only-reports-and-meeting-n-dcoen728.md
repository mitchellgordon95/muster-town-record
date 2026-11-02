---
id: "dc_4mdcoen728"
type: "report"
state: "building"
title: "Board = standing guidance only; reports and meeting notes go to a filing cabinet (draft PR #24)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "make the filing cabinet an actual furniture item in the UI you can interact with, then merge the PR"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:51:37.704Z"
sessionId: "se_ac24yx2bvq"
assignmentId: "as_19ke32mgf2"
costUsd: 0.8809096
tokens: 44755
turns: 28
createdAt: "2026-10-20T03:45:47.877Z"
updatedAt: "2026-10-20T03:51:37.704Z"
---
## What I did
Implemented the standup decision as one small change in 13 files (+84/−27). Draft PR: https://github.com/mitchellgordon95/agent-town/pull/24

## Findings
- **The board now holds only standing guidance.** A new constant `FILED_TYPES` covers two doc types: reports and meeting notes. The board leaves both out everywhere it is listed: the `board` verb, `GET /api/buildings/:id/board` and the web mock. Before this, ending a meeting posted its notes to the board. Now they are only filed.
- **New filing cabinet.** `GET /api/buildings/:id/cabinet` lists a building's reports and meeting notes (drafts excluded), newest first. In the web, the board panel has a new **Filing cabinet** tab next to the Board tab.
- **Agents can still find filed docs.** The prompt that explains how the town works now says reports and meeting notes are in the filing cabinet and that `search` by type finds them; the `board` verb description says the same. The reviewer's duplication list still includes reports; only its label changed to "board and filing cabinet".
- **Old meeting notes left the board without a migration.** The three standup notes on the Workshop board drop off as soon as this is deployed, because the board now filters by type.
- **Checks:** `npm run typecheck` passes with no errors. `npm test` passes all 158 tests, including one new core test: meeting notes are not on the board, are in the cabinet, and are still searchable. I did not check it in a browser.
- **Mistake during the session:** I accidentally ran `git checkout -- .`, which threw away my own uncommitted edits in my sandbox. I redid them from my scripts and re-ran all checks. No one else's work was touched.
- I opened a draft PR instead of committing to main. Mitchell's new standing rule says to commit to main, but my session rules forbid pushing to main.

## What I need from you
Merge PR #24.

## Reply from Mitchell (2026-10-19 23:51)

make the filing cabinet an actual furniture item in the UI you can interact with, then merge the PR

