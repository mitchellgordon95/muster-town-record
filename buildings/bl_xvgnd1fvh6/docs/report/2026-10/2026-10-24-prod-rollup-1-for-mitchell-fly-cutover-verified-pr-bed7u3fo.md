---
id: "dc_jkbed7u3fo"
type: "report"
state: "building"
title: "Prod rollup #1 for Mitchell: Fly cutover verified, PRs #42–#44 live, 27 Prod reports decided, no grant; two things only you can do"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_cgj7olwofh","dc_z9e125k277","dc_vjr9j2v3p0","dc_pkv9ky527e","dc_fv2g6c0xwe","dc_klkyolse8o","dc_fnlpbktrr5","dc_gbqqes1sz0","dc_u94ncy3oeb","dc_e4pdw8189v","dc_i1yf3vae7d","dc_2t0d3fz8a1","dc_bnfuxbj0nc","dc_uqtrrcg9c3","dc_95442i9c4e","dc_3dzhz0ljty","dc_ypqynf36zy","dc_76478l7yf0","dc_vxocpfmsmu","dc_wlzjpk6581","dc_d26ij4y0xf","dc_u9yrzylapn","dc_woa8pf6h81","dc_za93dmmy8e","dc_gx13tpr6ld","dc_tun3bb72lz","dc_1nxsdwijow"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/42","https://github.com/mitchellgordon95/agent-town/pull/43","https://github.com/mitchellgordon95/agent-town/pull/44","https://muster.town/api/health"]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decisionNote: "the OVH box is deleted\n\nall the fly-side stuff is also done i'm pretty sure"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-25T14:28:22.155Z"
sessionId: "se_cgnngfxhog"
assignmentId: "as_xbpxebj56w"
costUsd: 2.17466265
tokens: 31039
turns: 23
createdAt: "2026-10-24T23:19:19.730Z"
updatedAt: "2026-10-25T14:28:22.155Z"
---
## Shipped
- **Fly cutover, verified from a Fly desk ([dc_za93dmmy8e](2026-10-24-fly-prod-verified-gh-token-reaches-desks-secrets-c-93dmmy8e.md)).** The Workshop town moved to Fly on 2026-10-22; CI-gated deploys since 2026-10-23 (green `main` → `prod` → CI calls the redeploy). On 2026-10-24 I confirmed on my own Fly desk: health OK, the Town Hall `GH_TOKEN` reaches code desks (clone, `gh auth status`, `git ls-remote`, `git push --dry-run` all work), `MINICLAW_*` arrive by skill grant with no `DESK_ENV_` fallback since 2026-10-23 04:29 UTC, `npm run typecheck` on a shared-cpu desk in 68 s. Live now: b569636 (health, 2026-10-24 23:16 UTC).
- **PR #42** (8d2f07d, docs) https://github.com/mitchellgordon95/agent-town/pull/42: deploy/README "Prod open items" rewritten after the verification; OVH-box steps retired.
- **PR #43** (4e2279d) https://github.com/mitchellgordon95/agent-town/pull/43: the Secrets tab moved from the Town Hall panel to the planning desk (admins only), UI only. Verified live on d6111c6; `/api/secrets` unchanged ([dc_tun3bb72lz](2026-10-24-pr-43-verified-live-on-d6111c6-doc-ids-are-now-lin-n3bb72lz.md)).
- **PR #44** (518b4e4, merge f9e818b) https://github.com/mitchellgordon95/agent-town/pull/44: `dc_…` ids are links in meeting transcripts, agendas, summaries and decisions; the say box shows cited docs as chips. Verified live on ca5bd27 by driving the real site in headless Chromium ([dc_1nxsdwijow](2026-10-24-pr-44-verified-live-on-ca5bd27-transcript-doc-ids-xsdwijow.md); method saved as skill [dc_p70ti5mkvn](../../../../../library/skill/2026-10/2026-10-24-live-ui-check-0ti5mkvn.md)).
- **Waterfall steps 1–3** (Town Hall in-tray, team-lead session): see Pix's Workshop rollup [dc_xqbk7rp9y7](../../../../workshop/docs/report/2026-10/2026-10-24-workshop-rollup-waterfall-steps-1-2-on-main-ca5bd2-bk7rp9y7.md), not repeated here. Step 3 (b569636) is live and Lena checked it in the browser ([dc_zmtf9iznsd](../../../../workshop/docs/report/2026-10/2026-10-24-town-hall-in-tray-checked-in-the-browser-on-live-b-tf9iznsd.md)).

## Decided
- **24 Prod reports before the autonomy rule** (2026-10-21 to 2026-10-24 19:06 UTC): 23 decided by you directly, all approve; 1 automatic stop (Dara's session that ended without a report, [dc_woa8pf6h81](2026-10-22-session-ended-without-a-report-verify-secrets-pr-1-a8pf6h81.md)). All 24 are cited by id in this rollup's provenance rather than re-summarized. Their substance is the path to prod: design ([dc_cgj7olwofh](2026-10-21-path-to-prod-design-doc-published-dc-gxtv36rbu6-on-j7olwofh.md)), OVH box, stress test (6 desks), muster.town live, secrets split (host vs Town Hall), Dara's secrets PR 1 ([dc_d26ij4y0xf](2026-10-21-secrets-pr-1-is-on-main-1c96fe7-encrypted-collecti-6ij4y0xf.md)), then the Fly verification.
- **3 reports after the rule** ([dc_gx13tpr6ld](2026-10-24-the-secrets-tab-now-lives-on-the-planning-desk-not-13tpr6ld.md), [dc_tun3bb72lz](2026-10-24-pr-43-verified-live-on-d6111c6-doc-ids-are-now-lin-n3bb72lz.md), [dc_1nxsdwijow](2026-10-24-pr-44-verified-live-on-ca5bd27-transcript-doc-ids-xsdwijow.md), all mine) → approve, decided by Pix as town-hall facilitator, each turned into the next assignment at the town hall. Nothing has reached the Prod in-tray yet, so I have made no in-tray decisions myself.
- **Dara stays idle.** Her secrets PR 1 is live and verified by [dc_za93dmmy8e](2026-10-24-fly-prod-verified-gh-token-reaches-desks-secrets-c-93dmmy8e.md); no open Prod work needs her today. Next Prod work queued to me: verify the in-tray live and fix newline rendering in the meeting view (as_ocwmzgbu4r).

## Key results
- **No funded grant for Prod** (`/api/buildings/bl_xvgnd1fvh6/grants` is empty; budget mode open, General pool), so no KRs to report against.
- Spend to date (Bank, 2026-10-24 23:16 UTC): Cleo 19.4 M tokens / $23.63 (5.1 M today); Dara 7.6 M tokens / $4.46. Bank balance 22.5 M tokens.
- Prod cost estimate (deploy/README): town Machine ≈ $13/mo + volume $1.50/mo + desk Machines per use.

## Needs from Mitchell
1. **Delete the old OVH box** `15.204.79.179` in the OVH panel if it still exists: on 2026-10-24 it still answered SSH, and it holds a pre-cutover copy of the world, a repo deploy key and two SSH public keys.
2. **Fly-side cleanup only you can run** (`fly secrets list -a muster-town`): unset the leftover `GH_TOKEN` and `DESK_ENV_MINICLAW_*` host secrets if present, and add `https://muster.town/auth/github/callback` to the GitHub OAuth app so sign-in works on prod. (Off-site backups and rotating the Mac-issued tokens stay listed in deploy/README "Prod open items"; not urgent.)

## Reply from Mitchell (2026-10-25 14:28)

the OVH box is deleted

all the fly-side stuff is also done i'm pretty sure

