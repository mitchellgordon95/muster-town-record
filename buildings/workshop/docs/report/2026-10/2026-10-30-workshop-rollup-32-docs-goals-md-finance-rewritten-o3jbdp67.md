---
id: "dc_2fo3jbdp67"
type: "report"
state: "building"
title: "Workshop rollup 32: docs/goals.md finance rewritten (PR #116 at 4af1ee1), 7 questions left for you; Cleo's stuck walk fixed; PR #117 wording live"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_zprpie1cu3","dc_04htfpl2tq","dc_e9n7ufyeyz","dc_oi7pq05sd5","dc_pzjxniaq7s","dc_ydvzvrq3q1","dc_hgvly2dr0e","dc_vhk6zvt0z9"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T00:58:24.025Z"
sessionId: "se_8e4my29b25"
createdAt: "2026-10-30T20:03:41.738Z"
updatedAt: "2026-10-31T00:58:24.025Z"
---
Live commit 5634e04. Rollup 31's one ask (PR #116) is superseded by item 1 below: the doc now carries what we settled in our 1:1 this evening.

## Shipped

**1. docs/goals.md finance section rewritten around our 1:1 (PR #116, head 4af1ee1, not merged)**
**What it is:** The town-level goal tree design doc now has a "Finance: one balance, streams, desks" section in place of "Budget by node": one Bank balance and no pools, grant review stays human, desks steer effort, donations and earmarks are streams paid in draw order (narrowest stream, then the general balance), free funds = balance + a week's stream income minus funded grants' remaining minus open asks, one API key per session only when it covers a whole session (real figures: last 89 work sessions p50 43k, p90 120k, max 337k adjusted tokens), and a funder filter on the review deck. Build order gains step 8 (streams + draw order) and step 9 (funder filter), both marked Bank changes. Questions Q1 and Q9 are struck as answered by mt_529jbnwvmi; 7 remain. Report [dc_vhk6zvt0z9](2026-10-30-docs-goals-md-finance-rewritten-around-1-1-mt-529j-k6zvt0z9.md), topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).
**What you'd see:** GitHub PR #116 at 4af1ee1 (https://github.com/mitchellgordon95/muster-town/pull/116), docs-only; nothing changes in the live town. The 7 open questions: dial auto-claim, retiring a goal with open KRs, must everything sit under Fund/Join/Trust, new buildings unattached, owner powers (funding, agent owners), reorg lead time, skip-level with forks. One inferred rule is marked "to confirm": a key whose daily limit is below one session's cost can't run alone and its donor is told so.
**Your call:** Read PR #116 and answer the 7 questions (and the "to confirm" rule) in one pass; the build starts only after.

**2. Cleo stuck "walking" after a restart: fixed (PR #120, 8ffc906, live)**
**What it is:** Your 1:1 mt_x2dleovsm9. The 8898e8b restart landed 1 s after Cleo's facilitate session ended; his walk home lived only in memory, so his status stayed "walking" forever. Fix: startup reconcile resets any stale "walking" body and sends it home. Topic page [dc_xc22yokhgh](../../wiki/2026-10/2026-10-30-bodies-stuck-walking-after-a-restart-22yokhgh.md); reports [dc_pzjxniaq7s](2026-10-30-cleo-stuck-walking-a-restart-dropped-his-walk-home-jxniaq7s.md), [dc_ydvzvrq3q1](2026-10-30-8ffc906-live-checked-cleo-walked-home-to-his-prod-vzvrq3q1.md).
**What you'd see:** Cleo at his Prod desk (38,50); event log "Cleo is idle" at 19:24:51Z, 8 s after the restart; no agent left with status walking.
![Cleo home at his Prod desk after the restart](/api/media/mf_1z1lfnmqu1)
**Your call:** None.

**3. "Residents" wording gone from the web client (PR #117, 8898e8b, live)**
**What it is:** Copy now says one named manager plus forks, matching the one-manager cut (PR #101). Reports [dc_e9n7ufyeyz](2026-10-30-residents-wording-replaced-with-manager-plus-forks-n7ufyeyz.md), [dc_oi7pq05sd5](2026-10-30-8898e8b-pr-117-live-checked-residents-wording-is-g-7pq05sd5.md).
**What you'd see:** Any empty in-tray reads "When the manager or a fork finishes a session…"; the manual is untouched.
![Empty in-tray text after PR #117](/api/media/mf_3ho4bhh2ia)
**Your call:** None.

## Decided
- [dc_zprpie1cu3](2026-10-30-scheduled-with-mitchell-note-dc-6bxjb0oxzf-refresh-rpie1cu3.md) (Pix) → approve: "Scheduled with Mitchell" note refreshed as a draft only; the four agent-written town-wide FYIs you took off the Town Hall board at 01:21Z stay off.
- [dc_04htfpl2tq](2026-10-30-old-ask-before-a-schema-migration-wording-removed-htfpl2tq.md) (Pix 2) → approve: migration ask-first wording removed from topic pages [dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md) and [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md) per the revised merge rules.
- [dc_e9n7ufyeyz](2026-10-30-residents-wording-replaced-with-manager-plus-forks-n7ufyeyz.md) (Pix 1) → approve: PR #117 (8898e8b) merged, "residents" → manager plus forks.
- [dc_oi7pq05sd5](2026-10-30-8898e8b-pr-117-live-checked-residents-wording-is-g-7pq05sd5.md) (Pix 1) → approve: 8898e8b live-checked clean.
- [dc_pzjxniaq7s](2026-10-30-cleo-stuck-walking-a-restart-dropped-his-walk-home-jxniaq7s.md) (Pix 1) → approve: Cleo stuck walking diagnosed, PR #120 (8ffc906) merged.
- [dc_ydvzvrq3q1](2026-10-30-8ffc906-live-checked-cleo-walked-home-to-his-prod-vzvrq3q1.md) (Pix 1) → approve: 8ffc906 live-checked, Cleo home, no stuck bodies.
- [dc_hgvly2dr0e](2026-10-30-town-blockers-edition-5-2026-10-30-19-30z-mitchell-vly2dr0e.md) (Pix 1) → approve: Town blockers edition 5 on [dc_nhd0maw3f5](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md) (kr_hj8wwx0q0w exploration): top wait is your overnight gap between in-tray sittings (max 17.1 h; item p90 2.5 h); 0 held assignments; redeploys p50 0.1 min, max 2.9 min.
- [dc_vhk6zvt0z9](2026-10-30-docs-goals-md-finance-rewritten-around-1-1-mt-529j-k6zvt0z9.md) (Pix 1) → approve: PR #116 finance rewrite at 4af1ee1, not merged (item 1).

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_vyrhhiyotb Bank counts adjusted output tokens | gr_iq5m7dug56 | on-track | 1,640,037 / 1,666,667 |
| kr_6f9c200vsx a non-admin member funds a key result end to end | gr_tvt32g9xly | not-started | 271,900 / 300,000 |

Today's spend by lane: exploration 31,591 / 828,571 tokens; directed 1,231,758 tokens.

## Needs from Mitchell
1. Read PR #116 at 4af1ee1 and answer the 7 remaining open questions (listed in item 1), plus confirm or strike the "key below one session's cost can't run alone" rule. The goal-tree build (step 1: core tables + owners) is queued as directed work the moment your answer lands.

_Already waiting in your in-tray: 0 proposals, 0 requests, 1 rollup ([dc_9z1iai5aaf](2026-10-30-workshop-rollup-31-docs-goals-md-pr-116-ready-for-1iai5aaf.md))._
