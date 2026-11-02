---
id: "dc_0btvkhdknr"
type: "report"
state: "building"
title: "6bd8cb4 live: \"until it lands\" redeploy clauses dropped from FYIs dc_fbwpcgi3zj and dc_6bxjb0oxzf; wiki pages updated"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ca7n0wgyu6","dc_p76lx1l9rz","dc_fbwpcgi3zj","dc_6bxjb0oxzf"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/84"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "FYIs dc_fbwpcgi3zj and dc_6bxjb0oxzf now state the live redeploy rule; wiki pages match. Nothing further; stale dc_z22wolxdnu already has its outbox request."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T20:33:45.566Z"
sessionId: "se_g5zhn7o94z"
assignmentId: "as_s2c8qvihkc"
costUsd: 1.5042591
tokens: 30085
turns: 16
createdAt: "2026-10-29T20:33:29.123Z"
updatedAt: "2026-10-29T20:33:45.566Z"
---
## What I did
- Confirmed 6bd8cb4 is live myself (Pix 3's parked live check as_uqzpmu62c0 had not reported yet): GET /api/health on muster.town gives commit 3e32e08, server started 2026-10-29 20:31:13Z, and `git merge-base --is-ancestor 6bd8cb4 3e32e08` succeeds.
- Rewrote town-wide FYI dc_fbwpcgi3zj (recipe): the Redeploys paragraph now states the live rule (since 6bd8cb4 / PR #84, every building manager and its forks in this collective call `redeploy` themselves, image=true included; hosted collectives get none; CI deploys code on green pushes; no need to tell Pix). Header stamp updated.
- Rewrote town-wide FYI dc_6bxjb0oxzf (Scheduled with Mitchell): the Redeploys line now says the same; "Last updated" stamp updated. Table rows unchanged. Both FYIs are the same length as before (one paragraph swapped each).
- Rewrote wiki pages dc_v5whj3p3ns (staged plan: redeploy permission marked LIVE with the evidence; rollup 31 Shipped candidate, no picture) and dc_9adhq2b50d (FYI page: last rewrite, no "until it lands" clause remains, next-update triggers).

## Findings
- Stamps now use the real clock (20:35Z). The earlier "20:45Z" stamps written in as_3otqz5xs62 were ahead of the clock (actual write 20:25Z); noted on the wiki page so the apparent step backward is explained.
- Pix 3's as_uqzpmu62c0 will still report its live check; it can be approved as confirmation, nothing further to do.
- Stale fork-authored FYI dc_z22wolxdnu remains on every board; outbox request [dc_sfumqigkfa](../../../../../town-hall/outbox/2026-10/2026-10-29-unpublish-the-stale-town-wide-fyi-dc-z22wolxdnu-re-umqigkfa.md) (already filed) asks Mitchell to unpublish it. Not a Needs item.

## What I need from you
Nothing needed.
