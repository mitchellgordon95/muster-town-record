---
id: "dc_yr8iixkrnn"
type: "report"
state: "building"
title: "Blog confirmation mail sends live (200); PR #459 waiting on CI"
authorId: "ag_azf0q48qrd"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T21:47:18.146Z"
sessionId: "se_c0jlrbs4mk"
assignmentId: "as_z1hgbbfs28"
costUsd: 0.47648029999999997
tokens: 23824
turns: 13
createdAt: "2026-11-15T21:47:18.122Z"
updatedAt: "2026-11-15T21:47:18.146Z"
---
## What I did
Retested the blog signup after Mitchell's BLOG_MAIL_FROM fix, opened PR #459 with the format fix, and rewrote topic page [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md). I'm parked until CI finishes on #459.

## Findings
- Health at 21:44:33Z showed commit b80f73c, startedAt 21:42:53Z. That restart is Mitchell's secret change; he answered at 21:43:03Z.
- 21:44:40Z, honeypot POST: 200 `{"ok":true,"confirm":true}`.
- 21:44:40Z, POST with delivered@resend.dev: **HTTP 200** `{"ok":true,"confirm":true}`. Resend accepted the confirmation mail. That is as far as an agent can verify. A real inbox clicking the confirm link has not been tested.
- PR #459 (https://github.com/mitchellgordon95/muster-town/pull/459) changes mail.ts:3 and docs/blog.md:54. Both now give the exact `Name <email@domain>` / `email@domain` format and the 422 that results otherwise. The stale `blog@mail.muster.town` example is gone. It also adds the log file docs/log.d/2026-11-15-juno-1-blog-mail-from-format.md. Typecheck is green. CI is pending; I'll merge it when I resume.

## What I need from you
Nothing needed.
