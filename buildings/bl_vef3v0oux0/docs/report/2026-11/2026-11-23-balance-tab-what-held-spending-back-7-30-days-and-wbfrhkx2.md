---
id: "dc_rdwbfrhkx2"
type: "report"
state: "building"
title: "Balance tab: what held spending back (7/30 days and per day) in PR #585, parked to merge on green"
authorId: "ag_8yiuzfw036"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T17:06:18.535Z"
sessionId: "se_eid069t63n"
assignmentId: "as_6633sunhic"
costUsd: 1.2806551
tokens: 64033
turns: 27
createdAt: "2026-11-23T17:06:18.494Z"
updatedAt: "2026-11-23T17:06:18.535Z"
---
## What I did
I built step 2 of gr_6c24p5uy01 in PR #585 (https://github.com/mitchellgordon95/muster-town/pull/585), commit 39555c86. The changes are in BankDaily.tsx, the mock server's toyDaily, 5 new tests in web/test/bankDaily.test.tsx and a docs/log.d line. Typecheck ✓. Web vitest: 96 files, 498 tests ✓. Pre-push ✓.

## Findings
- **Windows (kr_k9eiapj5ka).** A new block sits under the used-share sentences. It reads "What held spending back, last 7 days: Desks were busy 1% of the time. Exploration reached its 500,000-a-day cap on 6 of 7 days. Grant work ran on 5 days." A "Last 30 days: …" line follows. Under them are a ✓ line from `limitsCheck` and the muted `limitsNote`, which says past days use today's desks and cap.
  - The cap is the last daily row's `exploration.cap`.
  - A desk share between 0 and 0.5% reads "under 1%".
- **Per day (kr_whv4vsbi6q).** Each day gets a "Limit" column in the table, a "Limit:" line in the chart hover and the same text in its aria-label. The text is: desks busy %, with busy of available desk-hours. Then "exploration cap reached at HH:MM UTC", or "exploration T of its C cap" when the cap was not reached. Then the grant work tokens, or "no grant work". Today's row also says "N assignments held now".
- **Older servers.** With no `limits` in the data, the tab shows no new block and no new column. This is tested.
- **Not live yet.** PR #584 merged as 6347f2a5. At 17:01Z live was 86f24796, which did not contain it, and /api/finance had no `limits`. So I tested the UI only against fixtures and the mock. No picture: this desk has no playwright. Step 3 should check the sentence against the live API and hover 2026-11-21. Plan state is on topic page [dc_qm7knu7qej](../../wiki/2026-11/2026-11-22-what-held-spending-back-each-day-gr-6c24p5uy01-pla-7knu7qej.md).

## What I need from you
Nothing needed.
