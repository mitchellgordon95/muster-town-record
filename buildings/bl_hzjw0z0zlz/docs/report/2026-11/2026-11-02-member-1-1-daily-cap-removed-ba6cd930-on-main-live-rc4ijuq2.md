---
id: "dc_q0rc4ijuq2"
type: "report"
state: "building"
title: "Member 1:1 daily cap removed (ba6cd930 on main); live check parked on its deploy"
authorId: "ag_an7tdohip8"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["mt_hlizi9wxxc","dc_ckzkpsahhv"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "ba6cd930 on main, suites green; its live check already waits on the queue as as_weo22cmyku (deploy ba6cd930). Nothing more to assign from this report."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T02:35:37.770Z"
sessionId: "se_n7foi91llr"
assignmentId: "as_twlx52w3wm"
costUsd: 0.6191004000000001
tokens: 30955
turns: 15
createdAt: "2026-11-02T02:35:16.180Z"
updatedAt: "2026-11-02T02:35:37.770Z"
---
## What I did
Following Mitchell's 1:1 (mt_hlizi9wxxc), I removed the per-member limit of one new 1:1 a day. It is one commit straight to main: **ba6cd930**, which is on origin/main. Typecheck passes, and the core (658), server (257) and web (233) tests all pass. Topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) is rewritten.

## Findings
- **Core** `packages/core/src/meetings.ts`: `MEMBER_ONE_ON_ONES_PER_DAY` is deleted, along with its export in index.ts. The 409 "You already opened a 1:1 today…" refusal in `createOneOnOne` is gone too. A member's second new 1:1 on the same day now opens.
- **Test** `packages/core/test/one-on-one.test.ts`: the cap assertions are replaced. The test now checks that a second new 1:1 in another building opens, and that a new 1:1 with the same manager opens after the member ends their first one.
- **Web**: the sentence "Members open one new 1:1 a day." is removed from the Talk callout in `AgentPanel.tsx`, and the comment in `oneOnOne.ts` is updated to match.
- **Docs**: the cap is removed from `docs/manual.md` (two places) and from `README.md`.
- **Left alone**, as asked: who may open a member 1:1, `oneOnOneMemberBlock`, and the "new member" callout. Proposal gr_cuobjlny6r is redesigning those.
- The "second-1:1 refusal" check in outbox add-on [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md) no longer applies.
- **Not live yet**: at 02:34Z the live server was still on dab5b9b. When this session resumes on deploy, it will check that the served main-*.js no longer contains "one new 1:1 a day".

## What I need from you
Nothing needed.
