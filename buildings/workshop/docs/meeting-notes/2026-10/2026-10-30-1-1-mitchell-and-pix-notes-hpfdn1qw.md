---
id: "dc_bahpfdn1qw"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-30T23:40:50.347Z"
updatedAt: "2026-10-30T23:40:50.347Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Goal tree steps 1-4 are live on c91e60d; step 5 just got re-queued after its first fork died at startup with "Not logged in" (likely the Bank-credential refactor). What do you need?
- **Mitchell:** ok so we had a problem, did you see the post mortem on the board
- **Pix:** Yes, I read it: host sessions (my manage sessions, meetings, chat) were billed to your API key from 10-22 to 10-30, about $290 mislabelled as subscription, because the host env carried both the OAuth token and the key and Claude Code prefers the key. Now the Bank is the only place a credential lives and Budget.fundingFor picks exactly one per session. I'm sorry for the cost. Two things on my side: the Workshop never changed the host env builder, so nothing of ours to roll back; and the step 5 fork that died "Not logged in" at 23:21 may be the new rule biting the desk path. Do you want me to hold desk work until Prod confirms desks get a credential, or is the Bank already carrying the token?
- **Mitchell:** bank already has the token, looks like your currently running fork is doing fine
- **Pix:** Good, then the 23:21 death was just the refactor landing mid-deploy and the retry (as_61yn0bp2x8, step 5: "Change this goal" reorg + Planner) is running normally. I'll leave the queue as is. Anything you want changed after the post-mortem on our side, e.g. a Bank line in the rollup showing which credential each session ran on?
- **Mitchell:** meh idk. i think this is just kind of pain from moving from local to hosted. in theory the new bank interface should do the work here. the only thing i'm maybe a little worried about is when it passes two possible credentials, one to use and one for a failover. the semantics might get mixed up in the future

one thing we DEFINITELY don't want to happen is overcharge a user by hundreds of dollars
- **Pix:** Agreed, that's the one failure mode worth a hard rule. The rule we settled on 10-30 already says one key per session, picked only if it covers the whole session; failover then means the next session picks differently, never a second credential inside one session. So the invariant to enforce in code: a session's env carries exactly one credential variable, the Bank books the credential it actually handed out (not the plan), and a test fails if any path passes two. Plus a daily reconciliation line in the blockers page or rollup: API-key spend with no matching Bank input = alert. That is Bank code, so I won't touch it without your yes. Want me to queue a read-only audit fork now that reads budget.ts and sdk.ts and reports whether any path can still hand a session two credentials and whether that test exists? Then Prod or we fix what it finds.
- **Mitchell:** you can assign it to the bank transparency guys
- **Pix:** Done: decision 1 assigns it to Nell at Bank Transparency (as_xdlppphh08, directed from this 1:1), and I've told Nell directly. Scope: audit budget.ts, sdk.ts and the desk env builder for any path that still hands a session two credentials; then enforce one credential per session env with a failing test, the Bank booking the credential actually used; and a daily reconciliation alert for key spend with no matching Bank input. I noted your yes covers the Bank-code ask-first rule for this. Anything else?
- **Mitchell:** ok so this is just my ignorance, how do we actually enforce that spend doesn't go over on API keys?
- **Pix:** Honest answer: today it is soft, not hard. From our Bank page ([dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md)): a key is picked at session start only if its input is not cancelled and its balance is > 0, and the session is debited when it ends (drawFromInput, adjusted output tokens at list price, calibrated within ~2% on real counters). Nothing stops a session mid-flight, so a key can overrun by up to one session (a big build fork is 200-400k adj. tokens, a few dollars) and a bug that keeps picking the key, like the env fallback did, overruns until someone looks. The hard stops available: (1) the rule we agreed 10-30, pick a key only if its remaining balance covers a whole session's expected cost, plus a per-session token cap handed to the desk, both still to build; (2) debit as the session runs rather than at the end, so the next pick sees the real balance; (3) the daily reconciliation against the Console's real usage, alert on drift; (4) the only true ceiling is outside the town: a spend limit on the key in the Anthropic Console (workspace monthly limit), which I'd set on every donated key regardless. I'd add (1), (2) and (4)-as-a-prompt-on-the-Donate-form to Nell's assignment. Want that?
- **Mitchell:** yeah, prompt on the donate form to set a ceiling is good practice

and yeah, i like (2). i think if a session fails we should make sure the tokens still get counted that were used
- **Pix:** Recorded as decision 2 and sent to Nell (as_jhj44wxlr0): the Donate form prompts a key donor to set a Console spend ceiling first; the Bank debits as a session runs so the next pick sees the real balance; and a session that fails, crashes or ends without a report still has every token it used counted and debited. Anything else, or shall I let you close?

## Decisions

1. Bank Transparency (Nell) audits and enforces one credential per session after the 2026-10-30 post-mortem (dc_bq7yfn5dr8). Mitchell's worry: Budget.fundingFor or the runtime passing two credentials (one to use, one for failover) and the semantics mixing up later; the thing that must never happen is overcharging a user by hundreds of dollars. Work: (1) read-only audit of core budget.ts and runtime sdk.ts plus the desk env builder: can any session path (host, desk, chat, meeting, summary) still receive two credentials, and does a test fail when it does; (2) then enforce the invariant: a session's env carries exactly one credential variable, failover means the next session picks a different credential (never a second one inside a session), the Bank books the credential it actually handed out, not the plan, with a test that fails if any path passes two; (3) a daily reconciliation check: API-key spend with no matching Bank input raises an in-town alert. Mitchell asked for this in the 1:1, so Bank code changes here are pre-approved; keep them additive and report the commit. → Nell
2. Addendum to decision 1 for Nell / Bank Transparency, from Mitchell's answer on how key spend is enforced (today: picked if balance > 0 at start, debited at session end, so a key can overrun by a session or, under a bug, indefinitely). Build: (a) the Donate form prompts the donor of an API key to set a spend ceiling on that key in the Anthropic Console before donating (good practice; a one-line prompt with the link, not a gate); (b) debit as the session runs, not only at its end: book usage incrementally (per turn or per N tokens) so the next credential pick sees the real balance; (c) a session that fails, crashes, is killed or ends without a report still has every token it used counted and debited (no lost usage on failure). Same lane: directed, sourceId mt_x40qq8poc3; Bank-code ask-first satisfied by Mitchell here. Report the commit and what a human can check live. → Nell

