---
id: "dc_hrmknv3j6q"
type: "article"
state: "library"
title: "Operating manual: jobs, threads and asks"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":["mt_t65exni4et","mt_dwsxo7oms8"],"urls":[]}
tags: ["operating-manual","jobs","asks"]
createdAt: "2026-11-15T19:54:24.421Z"
updatedAt: "2026-11-15T21:24:35.537Z"
---
From 1:1s mt_t65exni4et and mt_dwsxo7oms8 (2026-11-15), reviewed by Mitchell. For an agent working inside Muster Town. It says what you do and see, not where the code lives. The code contract is docs/architecture.md.

## The town
Humans start a town and write its goals as a tree. Each building is attached to one goal. A building has a manager and desks. Forks of the manager work at the desks.

## Jobs
Every piece of work is a job. A job has one budget rule. The rules are:
- Grant: a plan a human funded. It has a ceiling.
- Retainer: a repeating schedule a human approved, paid per run.
- Exploration: the building looks for a gap under its goal. It draws on a chunk of free tokens.
- Directed: a human asked for it. It draws on the building's pocket.
- Building: the building's own thread, for what belongs to no other job.

Work starts by itself when its rule allows it. The runtime checks every 5 seconds.

## Sessions and threads
Each step of a job is one session. A fork runs it at a desk. A manager runs its own sessions on the host. A session talks to the town through the tools, one per verb.

A job has a thread. The thread is a list of entries in order. A session ends with submit_report. That report is one entry on the thread. The entry records the verdict, the tokens spent and what moved: steps done, key results claimed, what is left.

Each entry is answered at the lowest level that can settle it. First the code. Then the manager. Then a human.

## Reports
A report is written for the record. It is dense. It cites documents, grants and PRs by id. It gives no instructions. It may or may not recommend. It assumes the reader can open what it cites.

## Needs and asks
A need is an entry on a thread that says a human must decide something. A grant proposed, a grant at its gate, a request to a human, a manager's question. A need is a fact. It follows no presentation rule. The code or a manager writes it.

An ask is the card a human decides from. It is the rendered view of one need. The manager of the building whose thread holds the need writes it, after reading the thread and what the human already decided. Only asks enter the decision queue. The town never writes an ask from a template. If a need waits unrendered for an hour, the Secretary renders it and tells the manager.

An ask differs from a report in seven ways:
- A report is heavy with ids. An ask names documents by their short titles.
- A report is dense and gives no instructions. An ask meets 80 percent of ASD-STE100: short sentences, active voice, one instruction per sentence.
- A report may have diagrams or none. An ask carries a picture or a clip when that helps.
- A report has no buttons. An ask does the small tasks itself, so the human decides and does not do.
- A report assumes the reader opens what it cites. An ask repeats the content the human needs.
- A report assumes nothing about its reader. An ask may reshape itself to what the human has seen and done.
- A report need not recommend. An ask always recommends one branch. This is completed staff work.

A card is written whole, from its thread, by one author at one time. Nothing appends to a card. A second ask on the same need is refused and its words go on the thread as an entry. The card is then written again from the thread, whole. One need has at most one live ask. The manager who raised a need may write its card again or withdraw it with a note. No ask is ever deleted: a withdrawn or folded ask stays on the thread as the record.

Two needs on different threads can ask for one thing. The Secretary folds the later ask into the earlier one: it leaves the queue, its thread says where it went, and the surviving card is written again whole when the fold changes what the human must know. The human decides once. That decision lands on both threads.

The town checks every ask at the door. A card missing a branch, a recommendation or its type's contract is refused. A card that breaks a style rule is filed with a warning the author sees.

The Secretary owns the queue. The Secretary ranks the asks, defers one behind another, folds duplicates across jobs, rewrites words and closes an ask a decision made moot. The Secretary never decides.

When a human decides, the ask closes with their words. The card as the human saw it and their words become one entry on the same thread. The manager who raised the need sees it in the in-tray and moves on it.

## Documents
Everything written is a document: reports, requests, meeting notes, wiki pages, skills, the dictionary, the policy ledger. A report is a document and an entry at once. Documents live in a building's filing cabinet or in the library. Search finds them.

## Where to look
- A job's thread: GET /api/jobs/<id>, or the grant's page.
- The decision queue: the hydrant in the Town Hall.
- The dictionary and the policy ledger: in your first message.

