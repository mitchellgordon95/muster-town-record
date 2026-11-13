---
id: "dc_lsmeci1asz"
type: "note"
state: "building"
title: "Bend 2 for the town's pure cores: findings and recommendation (stay in TypeScript with property tests)"
authorId: "ag_neccb0gf3y"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_j5ut8najul"],"urls":["https://github.com/bendlang/bend","https://github.com/bendlang/bend/blob/main/guide/GUIDE.md","https://github.com/bendlang/bend/blob/main/CHANGELOG.md","https://github.com/bendlang/bend/releases","https://github.com/bendlang/bend/issues/1328","https://github.com/bendlang/bend/issues/808","https://bend-lang.com/install.sh","https://akitaonrails.com/en/2026/09/19/new-ai-language-just-released-bend-2/"]}
tags: ["bend2","pure-core","proofs","mt_msnjkpgwdb"]
createdAt: "2026-11-13T06:11:51.203Z"
updatedAt: "2026-11-13T06:11:51.203Z"
---
Assignment as_nqgjbx12ks, from decision 15 part 3 of Mitchell's 1:1 mt_msnjkpgwdb. Investigation only: no code in the repo. Checked on Mara 1's desk on 2026-11-13 (desk clock 06:05–06:15 UTC) against bendlang/bend at commit 9162bfe (2026-11-12), Bend **2.0.40**.

**Worked example missing.** The pointer to Mitchell's side project (request [dc_j5ut8najul](../../../../../town-hall/outbox/2026-11/2026-11-13-a-pointer-to-your-bend-2-side-project-as-the-worke-ut8najul.md)) had no answer when this started. Everything below comes from public sources and from running Bend myself.

**Recommendation: stay in TypeScript and use property-based tests.** Bend 2 works. It loaded from Node and its checker caught both bugs I planted in a model of our chain-of-command rule, in under a second. But it is eight weeks old, with 99 open issues, 36 of them about soundness. A proof would cover a hand-copied Bend model, not the TypeScript that runs, unless we ship compiled Bend behind an adapter that nothing proves. For invariants this simple, fast-check property tests on the TypeScript core give most of the safety. They cost nothing new to read for seven buildings' agents.

---

## 1. Can a Bend 2 core be loaded from Node?

**What the sources say**
- `bend file.bend -o f.mjs` emits "an ES module of its non-IO defs, for JS to import". Values cross as `{$: "Name", field: …}`, `Nat` is a JS number, and `Bool`/`String`/`U32` are native (guide/GUIDE.md "IO and Concurrency", bend2/main.ts header). There is also a Node loader hook (`node --import`) and a Bun plugin.
- "The JavaScript target ignores all that [parallelism] and just runs sequentially" (GUIDE.md "Parallelism").
- The CLI itself is TypeScript run on Bun (`#!/usr/bin/env bun`, bend2/*.ts, about 14,000 lines). The installer downloads a pinned, SHA-checked prebuilt binary (bend-lang.com/install.sh, VER 2.0.40).
- `--verdict` rechecks proofs with a small kernel written and proven in Lean (bend2/bendtt.lean). It needs Lean v4.34.0.

**What I checked myself**
- I ran Bend from the checkout with Bun 1.4.4 (npm `bun` package). `--check-only` on a small file took 0.3–0.6 s.
- The emitted `chain.mjs` is 6,471 bytes, with **no imports**, readable plain JS. Node v22.23.4 (our runtime) imported it and got correct answers. 10^6 calls of the transform on a 4-goal chain took 34 ms.
- **No checking at the boundary.** A JS array passed where a Bend `List` was expected crashed ("Cannot read properties of undefined"). An object passed where a `Bool` belongs (`{$:"False"}`, which is truthy) was silently read as true, and a wrong answer came back. The proofs hold only for well-formed inputs, so the adapter between our rows and Bend values carries no proof.
- `--verdict`: the Lean toolchain is **about 3.0 GB**. On the first try it filled the desk's 4.9 GB home disk, so I installed it in /tmp. It built the kernel, a 5.5 MB binary. Run directly on the `-o PROOF.bendtt` translation, the kernel printed ALL PROOFS CHECK in 4 ms. The `bend --verdict` wrapper itself died with "kernel terminated by SIGABRT", even on the guide's 10-line `add_zero` example. That may be my npm Bun, not the official binary; I did not dig further.

**What I infer**
- Yes, it can load from Node. That holds wherever Node runs, Fly or the OVH box alike: the `.mjs` needs no Bend at run time.
- A proofs-only CI check needs just the pinned `bend` binary, about 0.5 s a check. Adding the proven kernel adds a Lean install of about 3 GB, or a cached prebuilt kernel.

**What I don't know**
- Whether the JS target always matches what the checker proved. Closed issue #808 says "the checker proves size 4, JS returns 3". It is fixed, but it is that class of bug.
- Why the `--verdict` wrapper aborted here.

## 2. One proof: "every building gets exactly one answerer"

I wrote and checked this. It is a model of `ownerOf` (packages/core/src/goals.ts:117). A building's chain is its attachment goal, then each parent, with the root left out. The answerer is the first captained goal on the chain, else the root.

```python
# chain.bend
type Goal is Data:
  G{id: Nat, captained: Bool}
type Answerer is Data:
  At{g: Goal}
  Root{}
def answerer(chain: +List<Goal>) -> Answerer:
  match chain:
    case Nil{}:
      Root{}
    case Con{G{id, c}, rest}:
      match c:
        case True{}:
          At{G{id, True{}}}
        case False{}:
          answerer(rest)
type Building is Data:
  B{id: Nat, chain: +List<Goal>}
def command(bs: List<Building>) -> List<Answerer>:   # one answerer per building
  match bs:
    case Nil{}:
      Nil{}
    case Con{B{id, chain}, rest}:
      answerer(chain) <> command(rest)
# helpers ok / is_root / none_captained / count_b / count_a: plain matches, omitted
```
```python
# LAWS.bend
law one_each:        # exactly one answerer per building, none dropped
  for bs: List<C.Building>
  {C.count_a(C.command(bs)) == C.count_b(bs) : Nat}
law answerer_ok:     # the answerer is a captained goal, or the root
  for chain: +List<C.Goal>
  {C.ok(C.answerer(chain)) == True{} : Bool}
law root_iff_none:   # the root answers exactly when nobody on the chain captains
  for chain: +List<C.Goal>
  {C.is_root(C.answerer(chain)) == C.none_captained(chain) : Bool}
```
```python
# PROOF.bend: induction on the list, one case split on `captained`
def Laws.one_each(bs):
  match bs:
    case Nil{}:
      {==}
    case Con{C.B{id, chain}, rest}:
      %Laws.one_each(rest) : {1n+C.count_a(C.command(rest)) == 1n+_ : Nat}
      {==}
def Laws.answerer_ok(chain):
  match chain:
    case Nil{}:
      {==}
    case Con{C.G{id, c}, rest}:
      match c:
        case True{}:
          {==}
        case False{}:
          Laws.answerer_ok(rest)
# Laws.root_iff_none: same shape as answerer_ok
```
**Results**
- `bend PROOF.bend` printed ALL PROOFS CHECK, and the Lean kernel accepted the translation.
- **Mutation 1:** an uncaptained goal answers. It failed `answerer_ok`, and the error pointed at the exact line.
- **Mutation 2:** `command` drops every building after the first. It failed `one_each`.
- It took 3 checker rounds. Both fixes were about Bend's quantities (`+List` for a list kept inside `Data`), not about the logic.

**What I infer**
- "Total" comes almost free: Bend refuses non-terminating functions, and the type gives exactly one answerer per input.
- The hard part of the real invariant is not in this model. In TypeScript, `ancestors()` walks parent ids in a table, and termination depends on the table having no cycle. Bend can't take a parent table without fuel or an `@unsafe` def. Modelling the chain as a list assumes the tree is already acyclic.
- The same goes for the "one building per goal" rule from decision 13. It needs ids to be distinct and a lookup to be functional. I did not attempt those proofs.
- Ids are `Nat` here. Our ids are strings like `gl_…`. Base has `String` and a string-keyed `Map`, but I did not prove anything over them.

**What I don't know**
- How much harder the acyclic-table version and the distinct-ids version are. I would guess several times this one, but that is a guess.
- Whether open issue #1328 bites real code: "a bare constructor name as a match pattern is silently a catch-all binder whenever the datatype comes from another file". Our proofs match on constructors from another file. I used the braced form `C.G{…}`, which the issue does not describe.

## 3. Costs and maturity

**What the sources say (GitHub API and repo, read 2026-11-13)**
- **Age.** Bend 2's first release was v2.0.8 on 2026-09-18. The repo `bendlang/bend` reuses the Bend 1 repo, created 2023-08. 2.0.40 came out 2026-11-05, and there are 33 releases in 8 weeks.
- **Activity.** 50 commits in the last 30 days. The top contributor (VictorTaelin) has 901 commits, and at least 30 people have contributed. 25,016 stars.
- **Issues.** 99 open (11 labelled bug). A search for "soundness" returns 36 issues, open and closed.
- **Stability.** The README says the TypeScript checker "has no proof and may have bugs". It calls `--verdict` the check with mathematical validity. A mismatch between the two prints "Your proofs may or may not be correct, and we cannot validate them yet".
- **Library.** Base is small: numbers, Bool, Maybe, Result, List, Array, a string Map and Set, and the IO effects. There are no tactics; you write proofs by hand as rewrites and induction.
- **Recent fix.** In the 2.0.40 changelog, the checker used to hang for more than 900 s on one proof.

**What I infer**
- **Tokens.** This 3-law model took about 110 lines of Bend and 3 checker rounds, inside a session that also did the research. I can't separate the token count, so take this as an order of magnitude, not a number. A fast-check property test of the same three claims is about 30 lines of TypeScript in a file agents already read.
- **Upkeep.** In proofs-only mode, every change to the TypeScript core needs a hand-made matching change to the Bend model. Nothing checks that the two still match: the model is the drift the town's doc checks exist to prevent.
- **Second language.** Bend has affine quantities, kinds, no `if`, and matches only on parameters. Each of the seven buildings' agents would need `bend guide` (678 lines) in context before touching a proven core. The checker's errors were precise, which helps.
- **Toolchain churn.** Weekly releases mean pinning a version, and every bump risks a new checker behaviour.

## 4. Recommendation: stay in TypeScript with property-based tests

1. A Bend proof today would cover either a hand-copied model, which drifts from the TypeScript that runs, or compiled Bend reached through an unproven adapter that silently misreads bad input. For invariants as simple as "one answerer per building", a fast-check property test on the pure TypeScript core catches the same planted bugs.
2. The toolchain is eight weeks old. The checker carries open soundness issues, and the proven kernel adds a 3 GB Lean install. That is a poor base for a CI gate that seven buildings' agents must pass and read.
3. Revisit when Bend's checker is the proven kernel by default, or when an invariant appears that property tests can't reach: one over every possible history, not samples. A proofs-only pilot on one core would then be the first step.

**If Mitchell wants a pilot anyway (a possible second session, not started):** add `LAWS.bend` and `PROOF.bend` for the chain-of-command model next to the TypeScript transform from as_fts38a0zxd. Run the pinned `bend` 2.0.40 binary in CI as a non-blocking job, and measure for two weeks how often the model drifts from the TypeScript.

Files from this session are on Mara 1's desk at /tmp/bendwork/coc (chain.bend, LAWS.bend, PROOF.bend, chain.mjs). /tmp is a cache; the code above is the record.
