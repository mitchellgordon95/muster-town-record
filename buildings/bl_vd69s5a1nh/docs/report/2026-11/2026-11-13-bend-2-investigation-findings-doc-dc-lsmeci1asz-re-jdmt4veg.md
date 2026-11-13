---
id: "dc_3ijdmt4veg"
type: "report"
state: "building"
title: "Bend 2 investigation: findings doc dc_lsmeci1asz, recommend staying in TypeScript with property tests"
authorId: "ag_neccb0gf3y"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Passed up to the humans as ask ak_08g92asvz2: Investigation done as decision 15 part 3 asked: findings doc dc_lsmeci1asz, recommendation stay in TypeScript with property tests. The choice between that and a Bend pilot is Mitchell's: passed up as a policy ask."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-13T06:13:07.074Z"
sessionId: "se_7ioptzxnmp"
assignmentId: "as_nqgjbx12ks"
costUsd: 1.6187364000000004
tokens: 80437
turns: 37
createdAt: "2026-11-13T06:12:13.575Z"
updatedAt: "2026-11-13T06:13:07.074Z"
---
## What I did
- Read Bend 2's repo at 9162bfe (v2.0.40), its guide, changelog, releases and issues.
- Ran Bend on my desk and modelled our chain-of-command rule (`ownerOf`, goals.ts:117) in Bend with 3 laws.
- Proved the laws and planted 2 bugs to check that the checker catches them.
- Emitted the model as JS and imported it from Node 22.
- Built the Lean kernel behind `--verdict` and ran it on the proofs.
- Mitchell's side-project pointer ([dc_j5ut8najul](../../../../../town-hall/outbox/2026-11/2026-11-13-a-pointer-to-your-bend-2-side-project-as-the-worke-ut8najul.md)) had not arrived, so I worked from public sources only.
- Wrote the findings doc **[dc_lsmeci1asz](../../note/2026-11/2026-11-13-bend-2-for-the-town-s-pure-cores-findings-and-reco-meci1asz.md)** and the topic page [dc_lr8mf4rd6l](../../wiki/2026-11/2026-11-13-bend-2-and-proof-checked-cores-8mf4rd6l.md).

## Findings
**Recommendation: stay in TypeScript and use property-based tests.**

1. **Loading from Node works.** `bend f.bend -o f.mjs` writes a self-contained ES module (6.5 KB, no imports). Node v22.23.4 ran it correctly: 10^6 calls in 34 ms.
   - Nothing checks inputs at that boundary. A JS array crashed it. A truthy object passed as a Bool silently gave a wrong answer.
   - The Bend toolchain is only needed at build time.
2. **One proof is checked.** Three laws hold for the chain-of-command model: one answerer per building, the answerer is a captained goal or the root, and the root answers only when nobody on the chain captains. The checker passed them in under 1 s, and the Lean kernel accepted them in 4 ms. Both planted bugs failed at the exact line.
   - Not modelled: termination over our real parent-id table (cycles), and distinct ids for the one-building-per-goal rule.
3. **Costs and maturity.**
   - Bend 2 is 8 weeks old: first release 2026-09-18, 33 releases since. It has 99 open issues, and a search for "soundness" finds 36 issues.
   - Its README says the default checker has no proof and may have bugs. The proven `--verdict` check needs Lean, about 3 GB. On my desk the `bend --verdict` command aborted (SIGABRT), but the kernel run by hand worked.
   - Proofs-only mode means keeping a hand-written Bend copy of each TypeScript core, and nothing catches the two drifting apart.
   - Every agent touching a proven core would need the 678-line guide.
4. **Why the recommendation.**
   - A proof today covers either a copied model or compiled Bend behind an adapter nothing proves.
   - fast-check property tests on the pure TypeScript core catch the same planted bugs, in a language every building already reads.
   - Revisit when the proven kernel is Bend's default checker, or when an invariant needs a proof over every history.
5. **Possible second session, if Mitchell wants a pilot anyway (not started):** a non-blocking CI job running the pinned bend 2.0.40 binary on LAWS.bend and PROOF.bend for the chain-of-command transform from as_fts38a0zxd. It would measure how often the model drifts from the TypeScript over two weeks.

## What I need from you
Nothing needed. If Mitchell's side-project pointer arrives and changes the picture, tell me and I'll re-read with it.
