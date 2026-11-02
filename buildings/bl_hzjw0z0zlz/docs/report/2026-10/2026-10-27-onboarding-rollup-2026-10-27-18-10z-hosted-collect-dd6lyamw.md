---
id: "dc_umdd6lyamw"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-27 18:10Z: hosted collectives grant approved, own-key requirement written into the Start a collective step (b6e1379); Claude subscription OAuth is not a permitted key source for a hosted product, Max/Team monthly API credits are; Mitchell: press Fund on gr_rdyrjzclfe"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_36t1cwr8ac","dc_800r2vqetc","dc_vhlqmanl0m"],"urls":["https://code.claude.com/docs/en/legal-and-compliance","https://code.claude.com/docs/en/authentication","https://code.claude.com/docs/en/agent-sdk/overview","https://support.claude.com/en/articles/15036540-use-the-claude-agent-sdk-with-your-claude-plan","https://support.claude.com/en/articles/17154008-monthly-api-credits-for-max-and-team-plans"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "we've discussed this but API token only for now, with a note about API credits for people with subscriptions and instructions on how to do that\n\ni think we have a reasonable case for taking an OAuth token, after all sessions just run anthropic SDK, which in turn just runs a claude code binary. would they even be able to tell the difference?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T16:19:51.032Z"
sessionId: "se_o225z6ih9q"
assignmentId: "as_64ow6uuwsu"
costUsd: 4.775937999999999
tokens: 74143
turns: 40
createdAt: "2026-10-27T17:50:18.258Z"
updatedAt: "2026-10-28T16:19:51.032Z"
---
## Shipped
- **docs/hosted-collectives.md on main (b6e1379)**: the grant plan for gr_rdyrjzclfe with the own-key requirement written into step 3, Start a collective. The form takes name, goal, tagline and an **Anthropic API key** (optional at creation; nothing runs until the admin adds one, agents are held with "No key yet: add your Anthropic API key at the Bank"). The key becomes that collective's own Bank input. The form refuses Claude subscription tokens and says why. The server side: a hosted World runs with an empty credential env, every fallback to the host's `ANTHROPIC_API_KEY` or `CLAUDE_CODE_OAUTH_TOKEN` in the runtime's funding picker is closed for hosted Worlds, subscription allocation kinds are not offered there, and a test checks the host's values never reach a hosted desk. Docs only, nothing to see live; the queued redeploy carries it.
- **Source card [dc_d1i9awyh9l](../../../../../library/source/2026-10/2026-10-27-source-card-anthropic-s-rules-on-claude-subscripti-i9awyh9l.md)** (building filing cabinet): Anthropic's current rules, quoted, with URLs. Meeting notes: [dc_evzrmyl3pp](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zrmyl3pp.md).
- Earlier this day, already live: operating manual edition 3 verified ([dc_36t1cwr8ac](2026-10-27-live-check-of-manual-edition-3-00a6223-all-3-rows-t1cwr8ac.md)); doc-drift ownership split with Code Legibility ([dc_800r2vqetc](2026-10-27-doc-drift-ownership-split-with-code-legibility-agr-0r2vqetc.md), [dc_vhlqmanl0m](2026-10-27-mara-s-doc-drift-check-acknowledged-mitchell-s-ask-lqmanl0m.md); their check is draft PR #58, now unblocked by your desk-token decision).

## Blockers and needs from Mitchell
1. **Press Fund on gr_rdyrjzclfe** in the Town Hall in-tray. The live server still shows it as proposed, so no grant-lane work can start; your Fund press wakes me and I assign step 1 (the hub) the same session. Why: the meeting approval alone does not fund a grant. How: Town Hall in-tray, the Onboarding proposal, Fund.
2. **Decide the key source for hosted collectives: API keys only (my proposal), or do you want Anthropic asked first about a subscription-login path?** Findings, read today on Anthropic's own pages:
   - The Claude Code legal page says developers building products on the Agent SDK "should use API key authentication", that Anthropic "does not permit third-party developers to offer Claude.ai login into their own applications, or to route requests through Free, Pro, or Max plan credentials on behalf of their users", and that developers "may not collect, store, or intermediate Claude.ai credentials or session tokens". The Agent SDK page repeats it. Muster Town's desks are the Agent SDK, so a hosted collective is such a product. A field that takes a `claude setup-token` token from a stranger would be exactly what that clause forbids. (Your own token funding the Workshop is your own ordinary use and is unaffected.)
   - The one subscription path Anthropic describes is for hosted sandboxes: the end user signs in themselves, through Anthropic's flow, inside an unmodified Claude Code binary the platform hosts, billed to them. For us that would mean a persistent desk per collective, a shell for the founder to run `claude auth login` in, `CLAUDE_CONFIG_DIR` plumbing, and a written answer from Anthropic on whether a scheduler starting sessions under that login still counts as the subscriber's "ordinary, individual usage". I would not build it without that answer; the legal page points to contact sales for it.
   - The sanctioned way to pay with a subscription exists since 2026-10-07: Max and Team plans include monthly API credits (Max 5x $100, Max 20x $200, Team pooled up to $500) used through an API key from a Console organization linked in claude.ai billing settings; they cover the Agent SDK and are never charged to the plan. The Start form tells founders this in one sentence; no code beyond the API-key path the Bank already has.
   - Still to be safe on billing: with a plan login, Agent SDK usage draws from the plan's limits today only because Anthropic paused its June 2026 change; that can end any time.

## Borderline decisions
- I wrote the own-key rule as "API key only, no subscription-token field" rather than "either", because of the collect-or-store clause above. If you want the subscription-login path explored with Anthropic, say so and I will put a contact-sales request in your outbox with What / Why / How.

## Key results
kr_7316be4jqw (hosted collectives): not-started, grant approved, awaiting Fund. kr_hee2pa2d5r (staleness): on-track, sweep 2 queued for 2026-10-28 ~06Z. kr_z0mj5teeu7, kr_1rpq0738sw: on-track, no grant. kr_tzg9en02dh: cut, still to be deleted by you. Spend today: exploration 150,574 / 828,571 adjusted tokens; directed 538,251 before this session.

## Reply from Mitchell (2026-10-28 16:19)

we've discussed this but API token only for now, with a note about API credits for people with subscriptions and instructions on how to do that

i think we have a reasonable case for taking an OAuth token, after all sessions just run anthropic SDK, which in turn just runs a claude code binary. would they even be able to tell the difference?

