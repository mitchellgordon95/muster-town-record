---
id: "dc_h9ke8i0rxo"
type: "report"
state: "building"
title: "Prod rollup #18: docs/self-host.md on main (one page from a Linux box to a town), directory API designed and proposed as gr_8cdix9mpye; the bring-up proof waits on a throwaway box"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_94iyf69ulf","dc_b4jww6hvat","dc_1rlphqgqwz"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T21:00:11.769Z"
sessionId: "se_dy7wot0fxa"
createdAt: "2026-10-29T20:34:09.003Z"
updatedAt: "2026-10-29T21:00:11.769Z"
---
main at 3e32e08; the items below are docs and design, so nothing needed a redeploy.

## Shipped
**1. docs/self-host.md: one page from a Linux box with a domain to a running town**
**What it is:** The self-host page key result kr_8qeqmy2wt8 asks for, written by a fork and committed to main at 93ccaaf (report [dc_94iyf69ulf](2026-10-29-docs-self-host-md-on-main-at-93ccaaf-one-page-from-iyf69ulf.md)). Six sections: requirements (2 vCPU / 2 GB from the stress test, Caddy for TLS), two ways to run it (from source under systemd with the unit written out, or Docker built from our Fly Dockerfile since there is no published image), every env variable with the file that reads it and the GitHub OAuth app steps, first sign-in, backups/restore/upgrades/logs, and a "register with the directory" stub pointing at the design. README's "Start your own collective" links to it.
**What you'd see:** GitHub, main, docs/self-host.md. Docs only, no picture. Tested on a desk: a fresh collective built from source answered /api/health ok, the admin token got the admin role on /api/me, /workshop/ served, and the OAuth redirect used the public URL. Not tested: Docker, TLS, a real GitHub sign-in. The page ends with 9 honest gaps; two small ones (the Fly entrypoint resets origin to upstream on every boot, so a fork's town redeploys from upstream; monitor FYIs need a building named "Prod") are on the queue as an exploration fix (as_h0jji5h3k1).
**Your call:** The key result's proof needs a throwaway box at a test domain. Your outbox has the request with three options (a Fly token for a throwaway app, a cheap VPS plus a subdomain, or Wright's VPS); the same box serves the directory grant's end-to-end step.

**2. Self-hosted towns directory: API designed and proposed as a grant**
**What it is:** Design [dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md) (report [dc_b4jww6hvat](2026-10-29-self-hosted-towns-directory-api-design-filed-dc-d6-jww6hvat.md)): register by DNS name, get a public token, prove control with a TXT record or a well-known URL, hourly re-check, listed while seen within 24 h, admin delete plus a block list. Proposed as gr_8cdix9mpye on kr_og03nxrkct (450k, three steps: register and list shape, verification and checker, end to end with the self-host town).
**What you'd see:** Nothing live yet; the proposal is in your Town Hall in-tray. API-only when built.
**Your call:** None beyond the proposal already in your in-tray.

## Decided
- [dc_1rlphqgqwz](2026-10-29-grant-gr-uhh6u39vv9-desk-session-performance-700k-lphqgqwz.md) → approve (desk session performance grant gr_uhh6u39vv9 cut into steps 1-2 on the building queue; step 3 queued after real steal numbers exist)
- [dc_b4jww6hvat](2026-10-29-self-hosted-towns-directory-api-design-filed-dc-d6-jww6hvat.md) → approve (directory API design; grant gr_8cdix9mpye proposed from it)
- [dc_94iyf69ulf](2026-10-29-docs-self-host-md-on-main-at-93ccaaf-one-page-from-iyf69ulf.md) → approve (docs/self-host.md on main; box request to the outbox, gaps 2 and 7 to the queue)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_iwj8m0461p monitor + red alerts outside the town | gr_rntk0echpi | on-track: steps 1-2 live, forced test alert waits on the ALERT_* secrets (Dara's continuation) | 325,747 / 800,000 |
| kr_4pf0n8q9jl desk session performance (cpu, steal) | gr_uhh6u39vv9 | not-started: step 1 pending on the building queue | 55,400 / 700,000 |
| kr_og03nxrkct directory registration | gr_8cdix9mpye | proposed, awaiting your decision | 0 / 450,000 asked |

Today's spend by lane: exploration 0 / 828,571 tokens; directed 309,184 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_8cdix9mpye), 3 requests (dc_nwv9dy37ui, dc_nhw4i75len, [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._
