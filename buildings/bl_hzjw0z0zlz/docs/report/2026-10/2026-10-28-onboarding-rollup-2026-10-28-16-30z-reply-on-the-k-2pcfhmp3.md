---
id: "dc_a32pcfhmp3"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-28 16:30Z: reply on the key source: API key only is what's live (credits note + how-to in the Start form and manual); why an OAuth token field is still a no even if the traffic looks the same; staleness sweep 2 live and checked"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_pl62lxv5kz","dc_umdd6lyamw","dc_t12ifwxccc"],"urls":["https://muster.town/","https://muster.town/api/manual","https://code.claude.com/docs/en/legal-and-compliance","https://code.claude.com/docs/en/agent-sdk/overview","https://support.claude.com/en/articles/17154008-monthly-api-credits-for-max-and-team-plans"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "ok we'll keep API key only. let's also make a note that if they want to use their subscription key, they'll need to host their own muster town via the open source repository so we avoid liability"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T17:31:26.501Z"
sessionId: "se_7pq5eecsu9"
assignmentId: "as_sp5zqzrpql"
costUsd: 1.92553305
tokens: 38511
turns: 17
createdAt: "2026-10-28T16:24:34.592Z"
updatedAt: "2026-10-28T17:31:26.501Z"
---
## Shipped
- **Your first ask is already live, nothing to build.** Live commit 4a4abd8 contains c3b6e98 (Craig's step 4c, checked 5/5 in [dc_t12ifwxccc](2026-10-27-hosted-step-4c-live-check-all-5-items-pass-on-1ece-2ifwxccc.md)). Demo: https://muster.town/ → Start a collective: the key field is "Anthropic API key (optional)"; under it: "Your agents run on your Anthropic API key, billed to you by Anthropic; Muster Town never spends its own. On a Max or Team plan, first link a Console organization in claude.ai Settings > Billing so the plan's monthly API credits pay for it, then create a key there and paste it (how)." The "how" link is Anthropic's Monthly API credits article (17154008). Next line: "Claude subscription tokens (from `claude setup-token` or `/login`) are not accepted: Anthropic does not let a third party collect or store Claude.ai credentials." The manual (HUD "?", https://muster.town/api/manual) has the same under **Getting a key**, with the amounts (Max 5x $100, Max 20x $200, Team pooled up to $500). I confirmed both strings are in the live JS bundle and the live manual this session.
- **Staleness sweep 2 (4a4abd8) is live and passes 5/5** (Tae's check [dc_pl62lxv5kz](2026-10-28-staleness-sweep-2-4a4abd8-is-live-on-muster-town-a-62lxv5kz.md), approved): manual has Finance ($), objectives + Dashboard (▤) and "Closed as done" at 1,889 words; /skill.md sends unhomed visitors' reports to the Town Hall in-tray. Sweep 3 runs tomorrow ~05:45Z (Craig).

## Your question: "would they even be able to tell the difference?"
Short answer: on the wire, probably not, and that is not what protects us.
- **You're right about the mechanics.** The Agent SDK is, in Anthropic's words, "a library that runs the Claude Code binary", and that binary accepts a `setup-token` OAuth token from `CLAUDE_CODE_OAUTH_TOKEN`. It is exactly how the Workshop runs on your token today. A founder's token in a hosted desk would send the same requests you do.
- **The rule is about the act, not the traffic.** The legal page says developers "may not collect, store, or intermediate Claude.ai credentials or session tokens" (quoted in my source card [dc_d1i9awyh9l](../../../../../library/source/2026-10/2026-10-27-source-card-anthropic-s-rules-on-claude-subscripti-i9awyh9l.md)). A form that takes a stranger's token and keeps it in our Bank is that act, whether or not anyone notices. Your own token on your own server is "ordinary use" and is fine; the difference is whose credential we hold.
- **Who gets hurt if they do look.** The token belongs to the founder's Claude account, so enforcement lands on them (plan suspension, "may do so without prior notice"); the operator who stored it is you, under the Commercial Terms that hosting Claude Code for end users puts us on. Anthropic has enforced twice this year (third-party clients in January, OpenClaw moved to extra-usage billing in April). I don't know what they can see, but a server that runs many accounts' tokens round the clock from one Fly.io host is not a hard pattern to spot, and I would not build a product on the bet that nobody does.
- **The upside is small.** A Max or Team subscriber already pays nothing extra: the plan's monthly API credits cover the Agent SDK through a key, which is the path that's live. OAuth would only let them draw on plan rate limits instead, and that works today only because Anthropic paused its June 2026 change. The real gap is Pro: no credits, so a Pro founder needs a paid Console account. OAuth doesn't close that gap legitimately either.
- **The one sanctioned subscription path**: the page allows "an end user signing in to the unmodified Claude Code binary with their own Claude subscription, including where a platform hosts Claude Code". For us that means a persistent desk per hosted collective where the founder runs `claude auth login` themselves (code-paste flow); the credential stays in that container, never in our database. Two open items: a Fly desk per collective (your cost call), and a written answer from Anthropic on whether a scheduler starting sessions under that login still counts as the subscriber's "ordinary, individual usage". I'd want the answer before building; the legal page points to contact sales.

Recommendation: keep API key only, as you decided. If you want the subscription-login question put to Anthropic, say so and I'll put a contact-sales request in your outbox with What / Why / How.

## Blockers and needs from Mitchell
Nothing needed. The 7-step checklist is on the "Scheduled with Mitchell" board for 2026-10-29; I use its result to close gr_rdyrjzclfe.

## Borderline decisions
None.

## Key results
kr_7316be4jqw hosted: not-started on the goal, all five steps live, grant gr_rdyrjzclfe 974,437 / 1,000,000 tokens (closes on your checklist result). kr_hee2pa2d5r staleness: on-track, sweep 2 live, sweep 3 queued. kr_z0mj5teeu7, kr_1rpq0738sw: on-track, no grant. kr_tzg9en02dh: cut, still to be deleted by you. Spend today: exploration 80,139 / 828,571 tokens; directed 0 before this session.

## Reply from Mitchell (2026-10-28 17:31)

ok we'll keep API key only. let's also make a note that if they want to use their subscription key, they'll need to host their own muster town via the open source repository so we avoid liability

