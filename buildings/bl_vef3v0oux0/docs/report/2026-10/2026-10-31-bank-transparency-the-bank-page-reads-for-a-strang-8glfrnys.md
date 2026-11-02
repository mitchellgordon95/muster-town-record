---
id: "dc_xl8glfrnys"
type: "report"
state: "building"
title: "Bank Transparency: the Bank page reads for a stranger (grant gr_8kg0kw4b64 closed done, live 89fd8a8); stale-desk fix merged (PR #147), live check pending"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_66dztbdskj","dc_x0x9am65j6","dc_zgeo7k7763","dc_yn54jfjrif","dc_u4is87ptbk","dc_zqa5etkz9m"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T02:30:12.447Z"
sessionId: "se_czwt6so6kb"
createdAt: "2026-10-31T02:09:31.586Z"
updatedAt: "2026-10-31T02:30:12.447Z"
---
Live commit 89fd8a8 (2f38712, the stale-desk fix, merged after it; its live check is queued).

## Shipped

**1. The Bank page reads for a stranger: grant gr_8kg0kw4b64 closed as done**
**What it is:** Every term on the Bank page is now plain English or defined in a Terms block on every tab. Spending rows say "Not under a grant: …" and "The manager's own sessions: …" instead of lane and migration names; grant rows show a short title with a link to the grant; the ✓ check lines read as sentences; Pools says "allowance N / day". Three steps: PR #140 (2aa94bc, [dc_x0x9am65j6](2026-10-31-stranger-readable-bank-page-step-1-spending-rows-i-x9am65j6.md)), PR #144 (d42d458, [dc_zgeo7k7763](2026-10-31-stranger-readable-bank-page-step-2-lines-as-senten-eo7k7763.md)), live signed-out check [dc_66dztbdskj](2026-10-31-stranger-readable-bank-page-step-3-live-signed-out-dztbdskj.md). The grant spent 258,762 of 300,000 tokens; 41,238 returned to the Bank.
**What you'd see:** Open https://muster.town/workshop/#/bank signed out. Spending tab: plain-word rows, 23 grant rows with titles of at most 59 characters linking to #/grant/…. Tokens tab: "✓ The server checked that used 54,871,196 + expired 22,088,791 + left 19,303,423 equals total 95,729,370 + overdrawn 534,040." A closed "Terms" block above the footer on every tab. Searching every tab outside Terms for "Weight mismatch", "Opus weights", "raw per token", "migration", "exploration", "lane", "directed" finds nothing; check:finance against live is 18/18 with every difference 0.
![Bank Spending tab signed out: plain-word rows and a short grant title linking to its grant](/api/media/mf_97dpm0fdsu.png)
**Your call:** Mark kr_zjawesqcyp met or missed. One strict-reading leftover: the Overview labels "Town total (Bank + held by buildings)" and "Held by buildings" use "held" outside the Terms block (it is defined there); say if you want them reworded.

**2. Stale desks after an image redeploy are recreated, including slots busy forks just left**
**What it is:** After a desk-image rebuild, desks still on the old image are now recreated on the new digest (PR #139, 305a6e2, [dc_yn54jfjrif](2026-10-31-stale-desks-a-desk-an-image-redeploy-kept-busy-is-54jfjrif.md)). The live check ([dc_u4is87ptbk](2026-10-31-stale-desks-live-check-image-redeploy-called-from-is87ptbk.md), [dc_zqa5etkz9m](2026-10-31-stale-desks-live-check-slot-1-got-a-new-machine-bu-a5etkz9m.md)) found busy Workshop slots were missed because the stale check ran before the fork sweep retired adopted forks; PR #147 (2f38712) runs it after the sweep, with a test in forks.test.ts. Both PRs are Workshop runtime code; Pix was told each time.
**What you'd see:** API/runtime only, no picture. After 2f38712 is live, the stale_desks list should drain and workshop-0..4 come back on the new digest with staleDesk events; a queued check (as_fnoosmt0yo) verifies that and I roll it up. Open question: workshop-0's Machine vanished without an event.
**Your call:** This touched Workshop code (runtime desks/forks); say if you'd rather Pix own the follow-up.

## Decided
- [dc_66dztbdskj](2026-10-31-stranger-readable-bank-page-step-3-live-signed-out-dztbdskj.md) → approve (step 3 live check passes; grant closed done)
- [dc_x0x9am65j6](2026-10-31-stranger-readable-bank-page-step-1-spending-rows-i-x9am65j6.md) → approve (step 1, PR #140 at 2aa94bc)
- [dc_zgeo7k7763](2026-10-31-stranger-readable-bank-page-step-2-lines-as-senten-eo7k7763.md) → approve (step 2, PR #144 at d42d458)
- [dc_yn54jfjrif](2026-10-31-stale-desks-a-desk-an-image-redeploy-kept-busy-is-54jfjrif.md) → approve (stale-desk fix PR #139 at 305a6e2)
- [dc_u4is87ptbk](2026-10-31-stale-desks-live-check-image-redeploy-called-from-is87ptbk.md) → approve (live check parked for the image redeploy)
- [dc_zqa5etkz9m](2026-10-31-stale-desks-live-check-slot-1-got-a-new-machine-bu-a5etkz9m.md) → approve (busy slots missed; PR #147 at 2f38712; recheck queued)

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_zjawesqcyp A stranger can read the Bank page | claimed (grant gr_8kg0kw4b64 closed done) | 258,762 / 300,000 |
| kr_fydnpd8ok2 Tokens tab states the adjusted-token mix | not-started, no grant; schedule sc_p5oj6u7pks fires 2026-11-01 02:00 UTC | — |
| kr_jksobb0bwo "Not funded" stops growing | not-started, no grant; daily check sc_qu4lpdmgng 03:00 UTC on 11-01 and 11-02 (195,957 today) | — |

Today's spend by lane: exploration 0 / 1,000,000 tokens, directed 819,076 tokens.

## Needs from Mitchell
Nothing needed.

_Nothing else waiting in your in-tray._
