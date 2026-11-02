---
id: "dc_i2c7in8y77"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Mara — notes"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-27T06:00:18.598Z"
updatedAt: "2026-10-27T06:00:18.598Z"
---
# 1:1: Mitchell and Mara

Kind: one-on-one. Facilitator: Mara. Attendees: Mara.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mara:** Hi Mitchell — our building has no key results yet, so here are three drafts to keep or cut (a redeploy is waiting on my session, so I'll be brief):
1) CI on main stays green without reruns. Check: GitHub Actions for main, last 20 runs pass on first attempt (recent example of a flake: run 40454959781).
2) Every core server subsystem (runtime/wakes, assignments & lanes, grants, bank) has a short invariants doc in docs/ linked from AGENTS.md, each invariant named by at least one test. Check: AGENTS.md links resolve; grep the test names.
3) Docs don't drift from code: a CI check fails when AGENTS.md/CLAUDE.md/README reference a missing file, script or tool name. Check: the check exists in CI and is green on main.
Which do you want to keep, change or cut?
- **Mitchell:** yeah so i might add
- Increase human code legibility via architecture docs and diagrams

I like the maintaining of the core subsystems, their invariants, how they work together, etc.

i think also doing sweeps to identify other things that are happening in the code that would be much cleaner if we created an abstraction and added it to the core subsystems

and yes, you can have doc drift. note this is different from onboarding copy drift, which is something i gave to kelly. you can check with her to make sure you're on the same page
- **Mara:** Back after the restart. I've set four key results from what you said (they're on our board now):
1) Architecture docs + diagrams: docs/architecture.md with a diagram of how runtime/wakes, assignments & lanes, grants and bank fit together, linked from README and AGENTS.md.
2) An invariants doc per core subsystem covering how it works with the others, each invariant named by a test.
3) Abstraction sweeps: a sweep report listing repeated patterns, with at least 3 moved into a core subsystem on main.
4) A doc-drift CI check for AGENTS.md/CLAUDE.md/README (not onboarding copy, which is Kelly's). I'll check with Kelly so we don't overlap.
You didn't mention "CI green without reruns". Keep it or drop it? Also, should I start with a grant for #1 (architecture docs) or #2 (invariants)?
- **Mitchell:** you can keep the CI

if the grants are independent feel free to file both in parallel
- **Mara:** Done. CI-green-without-reruns is key result #5 (kr_cm5qb2wqh7). I filed the architecture-docs grant gr_z9xj51uox3: 400k tokens, Finn writes docs/architecture.md with Mermaid diagrams, merged as one PR, and you read it as the test human. I can't file both in parallel because the town allows only one open proposal per building. The invariants grant goes in as soon as you fund, counter or reject this one; the two are independent.
- **Mitchell:** ok record the decisions now?

also the building should be able to have multiple grants, i'll have another building take a look
- **Mara:** Recorded four decisions: 1) the five key results; 2) the architecture grant gr_z9xj51uox3 is filed, and the invariants grant follows once you decide it; 3) you'll have another building look at letting a building hold multiple grants; 4) I check with Kelly on doc drift vs onboarding copy (assignment as_yypkucv51o). Once multiple grants work, I'll file the invariants grant right away.

## Decisions

1. Building key results kept: architecture docs + diagrams (kr_dctpbbwtno), invariants doc per core subsystem (kr_bo4codoha8), abstraction sweeps into core subsystems (kr_doa59kdway), developer-doc drift CI check (kr_oubxzkl4n6, onboarding copy drift stays with Kelly), CI on main green without reruns (kr_cm5qb2wqh7).
2. Grant gr_z9xj51uox3 (architecture docs, 400k tokens, Finn) is filed for Mitchell to fund. The invariants-docs grant gets filed as soon as it's decided, because the building currently allows one open proposal.
3. Mitchell will have another building look at letting a building hold multiple open grant proposals.
4. Mara checks with Kelly that doc-drift (developer docs) and onboarding-copy drift don't overlap. → Mara

