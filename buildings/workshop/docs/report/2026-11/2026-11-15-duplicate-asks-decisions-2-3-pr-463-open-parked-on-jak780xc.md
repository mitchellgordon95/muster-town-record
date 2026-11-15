---
id: "dc_ytjak780xc"
type: "report"
state: "building"
title: "Duplicate asks (decisions 2-3): PR #463 open, parked on CI"
authorId: "ag_uy8va83meq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T22:15:43.120Z"
sessionId: "se_0ztilpublo"
assignmentId: "as_c90hwgtrpj"
costUsd: 5.574660799999999
tokens: 278733
turns: 37
createdAt: "2026-11-15T22:15:43.108Z"
updatedAt: "2026-11-15T22:15:43.120Z"
---
## What I did
I built Mitchell's decisions 2 and 3 from 1:1 mt_dwsxo7oms8 on top of the merged PR #455, then merged main in, which brought Pix 3's queue rows and Pix 1's queue health. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/463. Decision 4 is not in it; it is queued as as_3f4qsq15tt.

## Findings
**One need, one ask.** `createAsk` checks the need entry (`sourceEntryId`). For the town's own needs it also checks for a live card of the same type on the same target (`liveAskForNeed`).
- A second ask on the same need is refused. Nothing changes on the card. The second filer's words become one `ask-refused` entry on the thread, written once. The call returns the first ask with folded: true.
- One exception: a town placeholder card is replaced whole by an author's card.
- A manager's ask of a different type on the same target is its own need and gets its own card. A grant can now carry a credential need beside its proposal.
- `fileNeed` supersedes only a need of the same kind.

**Sources list gone.** It is removed from the schema, AskCard, review deck, rank read and queue. The DB column stays and is no longer written, so there is no migration. `legible.asksPerTarget.folds` now counts the refused entries.

**Manager.** `ask` with askId and the whole card (title, body, recommendation) rewrites its own building's ask. A card missing required structure is refused; style problems are kept as warnings. `ask` with askId, withdraw: true and a note retires the ask, answers its own entry and wakes nobody. Another building's ask is refused.

**Secretary.** `rank` fold [{askId, into, note}] sets the ask to folded and records `foldedInto` and an entry on the folded thread. The human's decision on the surviving ask is written on both threads.

**Tests.** The new duplicate-asks.test.ts (6 tests) passes. The affected core tests (44) and all 421 web tests pass. The full `check --fast` failed only on 3 export/publish worker timeouts under load, and those 3 files pass on their own. Typecheck and knip are clean.

**Manual.** [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md) already had the principle. Topic page: [dc_637ckogeqo](../../wiki/2026-11/2026-11-15-duplicate-asks-mt-dwsxo7oms8-decisions-2-3-7ckogeqo.md).

**What a human sees when two asks are filed on one need:** one card in the queue, unchanged. The second filer's words show as an entry on the job's thread. The card is marked THREAD MOVED for its owner to rewrite whole.

## What I need from you
Nothing needed.
