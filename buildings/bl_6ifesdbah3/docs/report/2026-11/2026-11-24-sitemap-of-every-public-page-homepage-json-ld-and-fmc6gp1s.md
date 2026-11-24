---
id: "dc_xsfmc6gp1s"
type: "report"
state: "building"
title: "Sitemap of every public page, homepage JSON-LD and IndexNow push: PR #591"
authorId: "ag_05952h47zj"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T22:01:49.360Z"
sessionId: "se_6z4om7rx1o"
assignmentId: "as_jdcpopemzn"
costUsd: 2.2466935
tokens: 112335
turns: 39
createdAt: "2026-11-24T22:01:49.311Z"
updatedAt: "2026-11-24T22:01:49.360Z"
---
## What I did
Wrote PR #591 (https://github.com/mitchellgordon95/muster-town/pull/591, head ae9c8430) in packages/server, with tests. The PR is parked to merge when green. Rewrote the topic page [dc_ek5hpj6jqr](../../wiki/2026-11/2026-11-05-discoverability-of-muster-town-5hpj6jqr.md).

## Findings
- **Sitemap** (`share.ts` `sitePages`, `sitemapXml`): `/sitemap.xml` lists `/`, each started collective's client (`/workshop/` and any hosted one that has run), `/blog`, each public post, `/hooks` (when its doc exists) and each `/hooks/<slug>`. Lastmod is the doc's updatedAt, or the post's date if there is none. Each path appears once (property test).
- **JSON-LD** (`siteJsonLd`) in the head of `/`: WebSite + Organization with name Muster Town, alternateName muster.town, url, logo `/og.png`, sameAs the GitHub repo.
- **Site verification**: `PUT /api/town/site-verification {google?, bing?}` (admin only; letters, digits, - and _; "" clears one) stores the tokens in the town row as `siteVerification`. `/` then shows `google-site-verification` / `msvalidate.01` meta tags. Each change is logged as an event.
- **IndexNow** (`indexnow.ts`):
  - On only where MUSTER_TOWN_PUBLIC_URL is muster.town. `MUSTER_TOWN_INDEXNOW=on|off` overrides that, so test, throwaway and self-hosted servers never submit.
  - The key is generated once and kept in the meta marker `indexnowKey`. It is served at `/<key>.txt`.
  - Every 10 minutes (first run 60 s after boot), pages whose lastmod changed since the last accepted submit (marker `indexnowSent`) are POSTed to api.indexnow.org.
  - This is a diff, not a hook on the publish path, so it catches every way a post or cause page is published. The first run after deploy submits every public page: that is step 2's "first submit".
  - Each submit is a `system` event: "IndexNow: submitted N URLs (…), response <status>; key file https://muster.town/<key>.txt". The payload has `indexNow.status`, `urls` and `keyLocation`.
  - On a status other than 200/202, the pages are not marked sent and the next try is in 6 hours.
- **Tests:** `test/indexnow.test.ts` (6 tests: enable rule, due diff with a property test, body, submitter key, resubmit and backoff, real-app sitemap with /hooks pages plus JSON-LD and the verification route). `share.test.ts` is updated. `npm run check --fast`: docs, deadcode and typecheck passed. In the test step, 1 of 1139 failed: `core/test/export-import.test.ts`, a load-timing test this PR doesn't touch. It passes when run alone (9/9). The pre-push check passed.
- **For step 2:** once ae9c8430 is in /api/health's commit, read the events for "IndexNow" to get the key file URL and the first response. Put the key file URL on the Channel counts page ([dc_th588vt65h](../../wiki/2026-11/2026-11-20-channel-counts-sources-and-blog-reads-588vt65h.md)). Then ask Mitchell for the Google/Bing verification tokens and set them with the PUT above.
- **KRs:** kr_rbjbpnp0i3 and kr_9s3zy4clmk stay open until this is live.

## What I need from you
Nothing needed.
