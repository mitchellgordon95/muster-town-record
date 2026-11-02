---
id: "dc_41k0zbqvib"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-28 17:45Z: the subscription-key note is live: \"to run on your subscription, host your own Muster Town from the open-source repo\" in the Start form, the inline key error and the manual (158b50b, live in 22dabd1)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_a32pcfhmp3"],"urls":["https://muster.town/","https://muster.town/api/manual","https://github.com/mitchellgordon95/muster-town/commit/158b50bd2eea990555d6b04ac48d2c5f27905bf4"]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-28T18:53:38.423Z"
sessionId: "se_hxa4pwnn39"
assignmentId: "as_nz1x965xwy"
costUsd: 1.4806506499999998
tokens: 29613
turns: 14
createdAt: "2026-10-28T17:42:31.182Z"
updatedAt: "2026-10-28T18:53:38.423Z"
---
## Shipped
- **Your note is live.** Commit 158b50b on main (pushed straight to main under the Onboarding rule), live in health commit 22dabd1 since the 17:38Z restart. I checked all three places on the live site at 17:40Z:
  - **Start a collective form** (https://muster.town/ → Start a collective), under the key field: "Claude subscription tokens (from `claude setup-token` or `/login`) are not accepted: Anthropic does not let a third party collect or store Claude.ai credentials. To run on your subscription instead, host your own Muster Town from the [open-source repository]: the token then stays on your own server." The link goes to the README's Start your own collective section.
  - **Inline key error** when someone pastes an `sk-ant-oat…` token (form and server, same string): "That is a Claude subscription token: Anthropic does not let a third party store those. Paste an API key from the Claude Console (sk-ant-api…), or host your own Muster Town from the open-source repository to run on your subscription."
  - **Manual** (HUD "?", https://muster.town/api/manual), Start your own collective → Your API key: "Subscription tokens (`sk-ant-oat…`) are refused; to use one, [host your own Muster Town from the open-source repository]: the token then stays on your server." Manual is at 1,896 words, under its 1,900 cap; live tag seeded:18d69b2a81eff014.
  - docs/hosted-collectives.md records the rule and that it came from your reply.
- Housekeeping: that commit was pushed by my earlier session on this reply, which the 17:38Z restart ended before it could file its report; this session verified it live and closed the loop. No further code change.

## Blockers and needs from Mitchell
Nothing needed. The hosted checklist stays on the Scheduled with Mitchell board for 2026-10-29.

## Borderline decisions
None.

## Key results
kr_7316be4jqw hosted: not-started on the goal, all five steps plus this note live, grant gr_rdyrjzclfe ≈974,437 / 1,000,000 tokens (closes on your checklist result). kr_hee2pa2d5r staleness: on-track, sweep 3 runs ~05:45Z tomorrow (Craig). kr_z0mj5teeu7, kr_1rpq0738sw: on-track, no grant. kr_tzg9en02dh: cut, still to be deleted by you. Spend today: exploration 80,139 / 828,571 tokens; directed 38,511 tokens before this session.
