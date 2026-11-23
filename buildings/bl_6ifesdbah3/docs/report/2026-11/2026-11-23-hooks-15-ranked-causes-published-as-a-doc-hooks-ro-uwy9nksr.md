---
id: "dc_lquwy9nksr"
type: "report"
state: "building"
title: "Hooks: 15 ranked causes published as a doc; /hooks route in PR #570"
authorId: "ag_r4kesjrpmu"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:29:27.705Z"
sessionId: "se_fca2fulghy"
assignmentId: "as_tl0dx5h4qm"
costUsd: 1.9229285
tokens: 96146
turns: 33
createdAt: "2026-11-23T16:29:27.668Z"
updatedAt: "2026-11-23T16:29:27.705Z"
---
## What I did
Wrote 15 candidate causes with a stated ranking rule and published them as the Outreach note [Causes we'll test](../../note/2026-11/2026-11-23-causes-we-ll-test-15-collectives-that-could-exist-mxxm4cdb.md), tagged `hooks`. Opened PR #570 (https://github.com/mitchellgordon95/muster-town/pull/570). It serves that doc at /hooks like a blog post, with the About box and a signup (source `hooks`). Every blog page's nav links to it, and `hooks` is now a reserved collective slug. Because the page reads the doc, ranks and results change by rewriting the doc, not with a PR. I added a test in blog.test.ts and a section in docs/blog.md. The blog tests pass. In the full `check --fast` run, two worker-export tests (core export-import, publish) failed. The same 3 files pass when run alone with my change, so I think those failures came from load, not from my change. Topic page: [dc_5rr8n7dqf8](../../wiki/2026-11/2026-11-23-hooks-ranked-causes-r8n7dqf8.md).

## Findings
- **Ranking rule:** score = 2×Pull + Reach + Fit + Gap, each scored 1–3. Pull counts double because it is our only evidence of demand. Ties go to higher Pull, then a post before 20 emails, then higher Reach.
- **Pass thresholds:** one post needs ≥10 signups in 7 days (≥5 for small venues). 20 personal emails need ≥3 positive replies (15%). For comparison, cold sales email gets about 0.45–3% replies ([dc_w5hqe5lnao](../../note/2026-11/2026-11-23-explore-2026-11-23-hooks-goal-has-no-list-and-no-t-hqe5lnao.md)).
- **Top two:**
  1. **Complex PTSD and dissociation research** (13). Trauma Town is registered but not started (/api/collectives), and Mitchell named this cause. Test: one post in r/CPTSD or a similar forum, with moderator permission. Pass: ≥10 signups. Its landing page should say: "A collective where people living with C-PTSD/dissociation, clinicians and researchers steer AI agents doing literature synthesis in public, on a shared budget. Sign up to join, captain, or fund it." It should link Trauma Town (/trauma/) as the collective waiting for a founder.
  2. **Climate adaptation data for one region** (12). Mitchell named climate. Test: 20 emails to climate researchers. Pass: ≥3 positive replies. Its landing page should say: "Agents gather, clean and map public flood/heat/drought data for one named region, steered by climate researchers. Sign up to captain or contribute."
- Next by score: endometriosis (11), Long COVID/ME-CFS (11), city meetings and budgets (10), critical open-source maintenance (10).
- **Gotchas for step 2:**
  - mailing-list.ts `SOURCE` regex rejects `:`, so `hook:trauma` would be stored as `index`. Widen the regex to meet kr_fvyqcxxw69.
  - Put the landing pages at /hooks/<slug>, because /trauma/ is the collective's own path.
- Scores and "gap" judgments are our guesses, and the page says so. I measured no demand numbers.

## What I need from you
Nothing needed.
