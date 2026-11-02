---
id: "dc_v4iirqajou"
type: "wiki"
state: "building"
title: "Self-hosted towns directory"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_xvgnd1fvh6"
createdAt: "2026-10-29T04:26:55.780Z"
updatedAt: "2026-10-30T00:00:10.154Z"
---
State on 2026-10-30 ~01:10 UTC. Origin: Mitchell's 1:1 mt_mqq87d7zoo (notes [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), note [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md)). Objective ob_kdym3851tm (Join). Registration is OPEN, with no approval step (Mitchell).

**Jurisdiction (Kelly, Onboarding, ms_yegpj7v9cq):** the homepage tiles belong to Onboarding (packages/server/src/home.ts collectives(); Prod never edits that file). They read GET /api/directory or `directory.list()`. Prod owns docs/self-host.md, register/verify, the list and the re-check. Kelly was told the list shape is live (ms_80rs0lyzfo).

**API design: [dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md).** Building rule: never gate a muster.town feature on a new fly.town.toml [env] line, because the town redeploy is code only. `directoryEnabled` is on where MUSTER_TOWN_PUBLIC_URL is muster.town.

**Step 1 is LIVE at c2bf441** ([dc_ie8yimj67s](../../report/2026-10/2026-10-29-directory-step-1-merged-pr-94-fde6cb2-migration-05-8yimj67s.md), [dc_o5qr5a4t8g](../../report/2026-10/2026-10-29-directory-live-check-fde6cb2-live-but-routes-404-d-qr5a4t8g.md), [dc_dgzxfdqhdg](../../report/2026-10/2026-10-29-directory-step-1-is-live-at-c2bf441-all-five-curls-zxfdqhdg.md)): migration 059_directory.sql; register, list, /.well-known/muster-town (from env MUSTER_TOWN_DIRECTORY_TOKEN). example.org is a pending row in prod; the checker deletes it 7 days after creation (~11-05).

**Step 2 is LIVE** (PR #102, merged c01dd81; health commit b380807 at 23:58Z; reports [dc_vhylfbvmen](../../report/2026-10/2026-10-29-directory-step-2-merged-pr-102-c01dd81-proof-check-ylfbvmen.md), [dc_ds6ociu3e9](../../report/2026-10/2026-10-29-directory-step-2-live-check-passes-on-b380807-cont-6ociu3e9.md) approved). Live curls: health `directory: {verified:0, listed:0, pending:1, lastTickAt:"2026-10-29T23:58:02Z"}`; POST /verify example.org → 200 `{status:"pending", proof:null, lastError:"no TXT record at _muster-town.example.org; https://example.org/.well-known/muster-town answered 404"}` (same body within 60 s); /verify on an unregistered host → 404; anonymous DELETE → 401; GET /api/directory → `{towns:[]}`.

How step 2 works:
- **net.ts:** `safeGet` (https only, SSRF blocklist checked inside the lookup, no redirects, byte cap). Gotcha: don't add `::ffff:0:0/96` to Node's BlockList, it blocks every IPv4 address. `resolveTxtProof`: ENOTFOUND/ENODATA mean no proof; any other error means "couldn't check", not a miss.
- **Delisting:** second proof miss at least 1 h after the first. Tests: test/directory.test.ts (79).

**Step 3 (the real-town proof) is BLOCKED on outbox [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) (open; do NOT re-ask Mitchell).** Correction to earlier revisions: NO desk can make a throwaway fly.dev town. FLY_STRESS_TOKEN was revoked on 10-27 and app muster-town-stress destroyed (page "Stress test: harness and results"); deploy/fly/throwaway.sh needs a new org-scoped Fly token, which is option (a) of that outbox request. Cleo queued step 3 to her own desk on 10-30 (as_wc9102dgx3) and cancelled it on finding this. When Mitchell answers the outbox (token, VPS + subdomain, or Wright's box), a team-lead session queues step 3 (~100k, lane grant gr_8cdix9mpye) with this sequence:
1. Bring the test town up (from docs/self-host.md where the option allows: that also serves kr_8qeqmy2wt8) and register its host.
2. Set MUSTER_TOWN_DIRECTORY_TOKEN (or the TXT record).
3. POST /verify: the town shows in GET /api/directory, health shows listed 1, lastTickAt < 10 min. Tell Kelly (ag_s1n1xknj8n) so Onboarding can test tiles on live data.
4. Remove the proof, park ≥ 2 h, confirm the delist.
5. Tear the test town down.

Stop for the grant: the list shows one verified town that isn't muster.town with lastSeenAt under 24 h; then close_grant + rollup. kr_esgajhpgiz is claimed from step 3 plus Onboarding's tiles.

**Self-host page docs/self-host.md (kr_8qeqmy2wt8):** on main since 93ccaaf; gaps 2 and 7 live at 9002d0f. The bring-up proof waits on the same outbox.
