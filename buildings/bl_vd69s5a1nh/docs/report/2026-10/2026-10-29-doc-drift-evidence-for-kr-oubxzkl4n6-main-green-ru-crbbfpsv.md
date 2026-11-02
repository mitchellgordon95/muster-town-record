---
id: "dc_i7crbbfpsv"
type: "report"
state: "building"
title: "Doc-drift evidence for kr_oubxzkl4n6: main green (run 40949851903), broken path in PR #86 turns CI red at check:docs (run 40950031071)"
authorId: "ag_umct8dqnus"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_pxx1swfqkf"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/86","https://github.com/mitchellgordon95/muster-town/actions/runs/40950031071","https://github.com/mitchellgordon95/muster-town/actions/runs/40949851903"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Evidence is complete: main green on attempt 1 with check:docs running, PR #86 proved a broken backticked path turns CI red at docs, PR closed and branch deleted. The plain-text-path gap is noted on the topic page; not needed for the KR. Goes into today's rollup with \"Your call: mark kr_oubxzkl4n6 met\"."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T20:36:26.300Z"
sessionId: "se_x6ha1gl6se"
assignmentId: "as_ckip0larms"
costUsd: 0.4160766
tokens: 20804
turns: 12
createdAt: "2026-10-29T20:36:02.249Z"
updatedAt: "2026-10-29T20:36:26.300Z"
---
## What I did
I checked that the latest main CI runs are green and that their check job runs check:docs. I opened a throwaway draft PR that adds a reference to a missing file in AGENTS.md, recorded the failing run, then closed the PR and deleted its branch. No changes went to main. I updated the topic page [dc_pxx1swfqkf](../../wiki/2026-10/2026-10-29-doc-drift-check-x1swfqkf.md).

## Findings
- **Green on main:** run 40949851903 on f904590 passed on attempt 1, and so did run 40949326791 on 3e32e08. In both, the `check` job's `npm run check` ran docs first. The log says "doc references ok: README.md, CLAUDE.md, AGENTS.md, skills/muster-town/SKILL.md, docs/manual.md, docs/invariants/*.md". The timing line was `check: docs 0s | deadcode 4s | typecheck 16s | tests 1m26s | total 1m47s`.
- **Red on a broken reference:** draft PR https://github.com/mitchellgordon95/muster-town/pull/86 ("doc-drift check proof (do not merge)"), commit 274d6e9, run 40950031071 failed. From `--log-failed`:
  - `AGENTS.md:27: path \`scripts/does-not-exist.ts\` doesn't exist`
  - `1 broken reference(s). Fix the doc (or the code) in this change; ...`
  - `check: docs 0s | total 0s | FAILED at docs`
  
  PR #86 is closed unmerged and its branch is deleted on the remote.
- **Gap:** the checker only sees backticked spans and markdown links. My first commit (62fe441) used a plain-text path, `scripts/does-not-exist.ts` without backticks, and check:docs passed locally. That run was cancelled when I pushed the second commit. The KR's check ("breaking a path reference makes it fail") holds for formatted references. If the KR should also cover plain-text paths, the checker would need a change. It isn't needed to mark the KR met.
- This evidence is ready for the next rollup. **Your call:** mark kr_oubxzkl4n6 met.

## What I need from you
Nothing needed.
