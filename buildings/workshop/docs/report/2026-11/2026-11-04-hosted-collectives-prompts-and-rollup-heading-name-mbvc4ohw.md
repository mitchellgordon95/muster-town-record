---
id: "dc_hrmbvc4ohw"
type: "report"
state: "building"
title: "Hosted collectives' prompts and rollup heading name their root captain (PR #347, parked on CI)"
authorId: "ag_gadhzbopf3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #347 (captainName(), muster byte-identical, hosted collectives get \"## Needs from <captain>\") parked on CI; its continuation as_odevx95320 merges if green (no redeploy) and parks on the deploy. The three small leftovers (submit_report.rollup field text, digest gap text, mock fixtures) are not worth a session now; they go into the topic page as follow-ups. Goes into rollup 47 with its live check."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:49:48.961Z"
sessionId: "se_34563o9mcx"
assignmentId: "as_xr0d4qc65c"
costUsd: 1.2692738
tokens: 63464
turns: 25
createdAt: "2026-11-04T19:49:40.761Z"
updatedAt: "2026-11-04T19:49:48.961Z"
---
## What I did
Found every "Mitchell" that reaches a hosted collective. Added `World.captainName()` and used it in those places. Added tests, ran `npm run check` in the foreground (green), and opened PR https://github.com/mitchellgordon95/muster-town/pull/347 (head 0b73eec5, marked ready). Rewrote topic page [dc_b6c5iylz06](../../wiki/2026-11/2026-11-04-repo-mode-hiding-deploy-pr-machinery-from-collecti-c5iylz06.md).

## Findings
- **Where the name reached a hosted collective:**
  - manager prompts (core/src/prompts.ts):
    - the in-tray rules
    - the escalation criteria
    - the "Your in-tray" header
    - the explorer brief
  - the checkpoint kickoff assignment (grants.ts)
  - the rollup validator's two error messages (verbs/docs.ts)
  - schema `ROLLUP_NEEDS_RULE`
- **Already fine:** the rollup parser already matched any `## Needs from <name>` (schema rollup.ts `ROLLUP_SECTIONS`). So the validator, old rollups and the Town Hall in-tray rendering are unchanged.
- **How the name is chosen:** `captainName()` returns "Mitchell" in muster mode. Otherwise it returns the root goal's captain's name (else the first admin's, else "your captain"). In muster mode "he/him" stays, so muster.town's prompts come out the same, byte for byte. A test asserts that the manager prompt with the captain passed in equals the default.
- **Tests** (core/test/repo-mode.test.ts):
  - a hosted world with captain "Ada" gets "## Needs from Ada" and no "Mitchell" in its manager prompt or in-tray block
  - its rollup with "## Needs from Ada" files
  - a rollup missing that section is refused with "Missing: ## Needs from Ada"
  - muster still says Mitchell, he/him
- **Left as is (small, could be a follow-up):**
  - the MCP `submit_report.rollup` field description in schema still says "## Needs from Mitchell" for every collective. It is a tool description, not a prompt, and the validator accepts any name.
  - the Secretary's digest schedule gap text
  - web mock fixtures and code comments
- **Your call:** none. The heading change does not touch Town Hall in-tray rendering.

## What I need from you
Nothing needed.
