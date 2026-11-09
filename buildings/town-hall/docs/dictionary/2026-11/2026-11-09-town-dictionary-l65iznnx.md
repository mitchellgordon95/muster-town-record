---
id: "dc_rcl65iznnx"
type: "dictionary"
state: "building"
title: "Town dictionary"
authorId: "ag_lywy3igvel"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: ["dictionary"]
createdAt: "2026-11-09T04:05:24.777Z"
updatedAt: "2026-11-09T04:05:24.777Z"
---
# Town dictionary

One meaning per word. Every manager's prompt pins these words, and the ask linter refuses an avoided word with its replacement. Edit a line here to change a meaning; the linter reads the Avoid → use list as it stands.

## Words

- **ask**: something only a human can do, stored with its type, target, branches and recommendation. The human decides it.
- **notice**: a state change with nothing to do: something shipped, a grant closed, a key result verified.
- **record**: what an ask or a notice came from: a rollup, a report, a grant plan. It is one click down from the card.
- **gate**: the point where a grant waits for a human: at its ceiling, or a step report whose forecast is past it.
- **ceiling**: the tokens a human funded a grant for. The grant runs to it and holds there, never before.
- **size**: a step's price class: S, M or L, priced by the collective's table. A step bigger than L is split.
- **verified**: a key result a human saw live, or one whose check the server ran and passed.
- **claimed**: a key result a fork's report or the manager says is done. Nobody has checked it yet.
- **unknown**: a key result with no evidence either way.
- **fund / counter / reject**: a human's three answers to a grant proposal.
- **adjust / cut**: a human's two answers at a gate: change the ceiling, or end the grant here.
- **hold**: a grant at its ceiling: new sessions on it wait for a human.
- **slate**: the Secretary's ranked set of money asks: fund these, hold these, skip these, and why.
- **ledger**: the policy ledger: one rule per line with its origin, pinned in every manager's prompt.

## Avoid → use

- top-up → adjust
- checkpoint card → gate
- approve a grant → fund
- approve the grant → fund
- kill the grant → cut
- decision card → ask

