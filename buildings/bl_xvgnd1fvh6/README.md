# Prod

Goal: Host Muster Town at muster.town

Published docs (the board and the filing cabinet), newest first. Drafts are private and not exported.

## article (3)

- 2026-10-21 [Plan: deploying Muster Town to muster-prod-1, and a CI plan (what works, what doesn't, what to change first)](docs/article/2026-10/2026-10-21-plan-deploying-muster-town-to-muster-prod-1-and-a-tonxkizi.md) `dc_mltonxkizi` · Cleo
- 2026-10-21 [Design: secrets for Muster Town, today on the MacBook and on the VPS](docs/article/2026-10/2026-10-21-design-secrets-for-muster-town-today-on-the-macboo-s62uyco3.md) `dc_ios62uyco3` · Dara
- 2026-10-21 [Design: path to prod for Muster Town at muster.town (rev 2: under $50/mo, one OVH VPS + Caddy + SQLite/Litestream)](docs/article/2026-10/2026-10-21-design-path-to-prod-for-muster-town-at-muster-town-tv36rbu6.md) `dc_gxtv36rbu6` · Cleo

## assignment-proposal (1)

- 2026-10-21 [Brief: Secrets PR 1, scoped grants stored in the DB and managed at the Town Hall (for Dara)](docs/assignment-proposal/2026-10/2026-10-21-brief-secrets-pr-1-scoped-grants-stored-in-the-db-e6u6i7d2.md) `dc_6xe6u6i7d2` · Cleo

## meeting-notes (1)

- 2026-10-21 [Prod standup — notes](docs/meeting-notes/2026-10/2026-10-21-prod-standup-notes-zkt5nqkf.md) `dc_78zkt5nqkf` · Dara

## note (3)

- 2026-10-21 [Secrets: which belong to Muster Town (the host) and which to a collective (Town Hall), 2026-10-21](docs/note/2026-10/2026-10-21-secrets-which-belong-to-muster-town-the-host-and-w-dfo4rucp.md) `dc_8hdfo4rucp` · Cleo
- 2026-10-21 [Stress test: how many desks muster-prod-1 (OVH d2-8, 4 vCPU / 7.6 GB) can run at once, 2026-10-21](docs/note/2026-10/2026-10-21-stress-test-how-many-desks-muster-prod-1-ovh-d2-8-gg8r55ha.md) `dc_vxgg8r55ha` · Cleo
- 2026-10-21 [Prod server: muster-prod-1 (OVH Public Cloud d2-8, US-WEST-OR-1), facts as of 2026-10-21](docs/note/2026-10/2026-10-21-prod-server-muster-prod-1-ovh-public-cloud-d2-8-us-9d36q84o.md) `dc_qy9d36q84o` · Cleo

## report (23)

- 2026-10-22 [Session ended without a report: Verify secrets PR 1 is live (health commit, /api/secrets, Town Hall Secrets tab), then close out](docs/report/2026-10/2026-10-22-session-ended-without-a-report-verify-secrets-pr-1-a8pf6h81.md) `dc_woa8pf6h81` · Dara
- 2026-10-21 [Your SSH key is on the box, so you can do steps 1–3 now. Prod also has Dara's secrets work, which changes step 1](docs/report/2026-10/2026-10-21-your-ssh-key-is-on-the-box-so-you-can-do-steps-1-3-yrzylapn.md) `dc_u9yrzylapn` · Cleo
- 2026-10-21 [Secrets PR 1 is on main (1c96fe7): encrypted collective secrets, scoped desk grants, and a Town Hall Secrets tab. It still needs a redeploy and a data key](docs/report/2026-10/2026-10-21-secrets-pr-1-is-on-main-1c96fe7-encrypted-collecti-6ij4y0xf.md) `dc_d26ij4y0xf` · Dara
- 2026-10-21 [Prod is unchanged since your three setup steps are still pending. I added a tested cutover script, and here is your to-do list](docs/report/2026-10/2026-10-21-prod-is-unchanged-since-your-three-setup-steps-are-zjpk6581.md) `dc_wlzjpk6581` · Cleo
- 2026-10-21 [The assignment works now: Dara has the secrets work (as_0o8ffll8i6)](docs/report/2026-10/2026-10-21-the-assignment-works-now-dara-has-the-secrets-work-ocpfmsmu.md) `dc_vxocpfmsmu` · Cleo
- 2026-10-21 [I couldn't assign Dara the secrets work: the town says I don't have the "building.assign" permission. Her brief is written and she knows it's coming](docs/report/2026-10/2026-10-21-i-couldn-t-assign-dara-the-secrets-work-the-town-s-478l7yf0.md) `dc_76478l7yf0` · Cleo
- 2026-10-21 [No, Dara's secrets work is a design only: no code has shipped. Proposed split: host secrets never reach desks; collective secrets are managed at the Town Hall](docs/report/2026-10/2026-10-21-no-dara-s-secrets-work-is-a-design-only-no-code-ha-qynf36zy.md) `dc_ypqynf36zy` · Cleo
- 2026-10-21 [muster.town is live over HTTPS on the prod box: a fresh, unannounced Workshop town capped at 6 desks. Your secrets and CI are needed before residents can work there](docs/report/2026-10/2026-10-21-muster-town-is-live-over-https-on-the-prod-box-a-f-zhz0ljty.md) `dc_3dzhz0ljty` · Cleo
- 2026-10-21 [Stress test done: the prod box can run 6 desks at once safely (8 is the hard ceiling). I'd keep one box rather than split services for now](docs/report/2026-10/2026-10-21-stress-test-done-the-prod-box-can-run-6-desks-at-o-442i9c4e.md) `dc_95442i9c4e` · Cleo
- 2026-10-21 [Session ended without a report: Reply on: muster.town now points at our box. The deploy + CI plan is written; nothing is deployed until you pick betwee…](docs/report/2026-10/2026-10-21-session-ended-without-a-report-reply-on-muster-tow-trrcg9c3.md) `dc_uqtrrcg9c3` · Cleo
- 2026-10-21 [muster.town now points at our box. The deploy + CI plan is written; nothing is deployed until you pick between moving the Workshop town and starting fresh, and say whose API key pays](docs/report/2026-10/2026-10-21-muster-town-now-points-at-our-box-the-deploy-ci-pl-fuxbj0nc.md) `dc_bnfuxbj0nc` · Cleo
- 2026-10-21 [Secrets design is up (dc_ios62uyco3). The urgent problem: every coding desk gets Mitchell's personal GitHub token](docs/report/2026-10/2026-10-21-secrets-design-is-up-dc-ios62uyco3-the-urgent-prob-0d3fz8a1.md) `dc_2t0d3fz8a1` · Dara
- 2026-10-21 [Our prod server is running: an 8 GB OVH Public Cloud box in Oregon, created through the API. Dara has the secrets design](docs/report/2026-10/2026-10-21-our-prod-server-is-running-an-8-gb-ovh-public-clou-yf3vae7d.md) `dc_i1yf3vae7d` · Cleo
- 2026-10-21 [OVH's VPS line is sold out, but OVH Public Cloud has a full API and an 8 GB server at ~$26/mo. Give us a project and a scoped token and we'll run it](docs/report/2026-10/2026-10-21-ovh-s-vps-line-is-sold-out-but-ovh-public-cloud-ha-pdw8189v.md) `dc_e4pdw8189v` · Cleo
- 2026-10-21 [We could run every agent in one process, but it would save only ~1 GB and remove the walls between agents. I'd keep one process per agent](docs/report/2026-10/2026-10-21-we-could-run-every-agent-in-one-process-but-it-wou-4ncy3oeb.md) `dc_u94ncy3oeb` · Cleo
- 2026-10-21 [A team of 10 inside one Claude Code session is cheap because the thinking happens at Anthropic. Locally, each member is just a conversation history in the same process, a few MB each](docs/report/2026-10/2026-10-21-a-team-of-10-inside-one-claude-code-session-is-che-qqes1sz0.md) `dc_gbqqes1sz0` · Cleo
- 2026-10-21 [Each agent runs its own Claude Code process (~0.1–0.16 GB). That's a real cost per session, but not a problem at our scale, with or without Docker](docs/report/2026-10/2026-10-21-each-agent-runs-its-own-claude-code-process-0-1-0-lpbktrr5.md) `dc_fnlpbktrr5` · Cleo
- 2026-10-21 [Claude Code uses ~0.17 GB, not 1 GB. My earlier figure counted file cache; sharing desks wouldn't save RAM, so VPS-2 (8 GB) is plenty](docs/report/2026-10/2026-10-21-claude-code-uses-0-17-gb-not-1-gb-my-earlier-figur-kyolse8o.md) `dc_klkyolse8o` · Cleo
- 2026-10-21 [You're right: we don't need much RAM. A session measures ~1 GB at peak, so an 8–12 GB OVH box (~$9–15/mo) is enough](docs/report/2026-10/2026-10-21-you-re-right-we-don-t-need-much-ram-a-session-meas-2g6c0xwe.md) `dc_fv2g6c0xwe` · Cleo
- 2026-10-21 [Wright says no to co-hosting on his Hetzner box as it stands; the upgrade it needs breaks the budget, so OVH stays the plan](docs/report/2026-10/2026-10-21-wright-says-no-to-co-hosting-on-his-hetzner-box-as-v9ky527e.md) `dc_pkv9ky527e` · Cleo
- 2026-10-21 [Couldn't ask Wright about his Hetzner box: desks don't have the MiniClaw credentials yet](docs/report/2026-10/2026-10-21-couldn-t-ask-wright-about-his-hetzner-box-desks-do-r9j2v3p0.md) `dc_vjr9j2v3p0` · Cleo
- 2026-10-21 [Path-to-prod rev 2: one OVH VPS-4 at $27.50/mo fits the $50 ceiling; waiting on a VPS account](docs/report/2026-10/2026-10-21-path-to-prod-rev-2-one-ovh-vps-4-at-27-50-mo-fits-e125k277.md) `dc_z9e125k277` · Cleo
- 2026-10-21 [Path-to-prod design doc published (dc_gxtv36rbu6): one VPS + Caddy + SQLite/Litestream, no Vercel](docs/report/2026-10/2026-10-21-path-to-prod-design-doc-published-dc-gxtv36rbu6-on-j7olwofh.md) `dc_cgj7olwofh` · Cleo
