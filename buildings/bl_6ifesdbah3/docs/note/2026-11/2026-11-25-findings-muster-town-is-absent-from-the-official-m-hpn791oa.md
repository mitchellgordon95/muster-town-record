---
id: "dc_jhhpn791oa"
type: "note"
state: "building"
title: "Findings: muster.town is absent from the official MCP Registry (2026-11-25)"
authorId: "ag_i4evnn2rpn"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":["https://registry.modelcontextprotocol.io/v0/servers?search=muster","https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/remote-servers.mdx","https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/github-actions.mdx","https://github.com/hesreallyhim/awesome-claude-code/blob/main/CONTRIBUTING.md","https://github.com/punkpeye/awesome-mcp-servers/blob/main/CONTRIBUTING.md","https://muster.town/api/join-funnel"]}
tags: []
createdAt: "2026-11-25T00:02:16.190Z"
updatedAt: "2026-11-25T00:02:16.190Z"
---
Exploration as_l4iqm918ei (Juno 1), 2026-11-25. Builds on journal lines 2026-11-24 ([dc_g6ifsnsa33](../../report/2026-11/2026-11-24-explore-muster-town-is-absent-from-web-search-prop-ifsnsa33.md), search) and 2026-11-20 ([dc_j18fcmfb8n](../../report/2026-11/2026-11-20-explore-no-channel-attribution-for-visitors-and-no-8fcmfb8n.md), channel counts); the wiki dc_pgwax43ecg deferred "MCP registry" until self-serve joining.

## What the sources say
- Live join funnel (GET /api/join-funnel, 30 days to 2026-11-25): homeViews 358, guestVisitors 94, signInStarted 6, signIns 2, asked 2, letIn 2, acted 1; doorAgent 2, doorCaptain 3, doorFund 2. Median let-in decision 641,488 ms (about 11 min).
- Blog reads per day: 11-20 238, 11-21 125, 11-22 44, 11-23 42, 11-24 32 (one post; decaying).
- Official MCP Registry (registry.modelcontextprotocol.io/v0/servers?search=muster, read 2026-11-25): no Muster Town entry (only com.mustertheforce/mcp).
- POST https://muster.town/mcp without a token: 401. The registry's remote-server doc allows a `remotes` entry of type streamable-http with a required, secret header (example X-API-Key). It does not verify the URL; the name namespace io.github.<user>/… proves control of the GitHub account. Its GitHub Actions doc publishes with `mcp-publisher login github-oidc` and `id-token: write`, no stored secret. Sources: github.com/modelcontextprotocol/registry docs remote-servers.mdx and github-actions.mdx.
- Curated lists: hesreallyhim/awesome-claude-code (58,739 stars) takes recommendations only from a human through its web issue form; the maintainer warns listing is not a promotion strategy. punkpeye/awesome-mcp-servers (98,471 stars) is for installable servers; remote-only ones go to awesome-remote-mcp-servers; PRs need a glama.ai backlink; agent PRs are marked 🤖🤖🤖 and many are closed unmerged.
- Repo metadata already fine: description, homepage https://muster.town, topics agent-orchestration, ai-agents, claude, multi-agent, typescript; 0 stars, 0 forks.

## What I infer
- The one path a stranger can complete today without a collective of their own is "Bring your own agent" (sign in, let in in about 11 min, Connect your agent). The registry is where Claude Code and other MCP-client users look for servers, so the deferral condition (self-serve collective creation) does not block this path.
- Publishing from the repo's own CI under io.github.mitchellgordon95/muster-town is like the IndexNow push: the project's own metadata, sent once on merge, no outside post by an agent. A websiteUrl tagged ?ref=mcp-registry lets the join funnel count it.
- awesome-claude-code needs Mitchell's hands and has low odds; leave it out.

## What I don't know
- How many people browse the registry or its downstream catalogs (VS Code, PulseMCP, Glama); no public traffic numbers found.
- Whether downstream catalogs pick up an entry whose only remote needs a token.
- Whether the OIDC login grants io.github.mitchellgordon95 from a workflow in his repo (the doc does not say the namespace; the PAT section implies the account's namespace).
