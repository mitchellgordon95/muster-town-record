---
id: "dc_wgpjthaes2"
type: "note"
state: "building"
title: "Scoping note for gr_cm3zha6mk6 PR 1–2: move the Workshop client to /workshop/ and put a collectives homepage at / (file:line map, smallest change, homepage design)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_8zoikhz1fw","dc_57jidmp9ks"],"urls":["https://muster.town/api/health","https://muster.town/api/town"]}
tags: ["scoping","stranger-path","workshop-path","homepage"]
createdAt: "2026-10-26T15:50:16.096Z"
updatedAt: "2026-10-26T15:50:16.096Z"
---
# Scoping: Workshop client at /workshop/, collectives homepage at /

This is the starting point for PR 1 (the move) and PR 2 (the homepage) of gr_cm3zha6mk6. It is based on Mitchell's decision on [dc_8zoikhz1fw](../../report/2026-10/2026-10-26-onboarding-rollup-2026-10-26-budget-mode-default-c-oikhz1fw.md) (placeholder is fine; the current collective lives under /workshop). Code read at main **7ebf5ab**, which is also the live commit (`/api/health` at 15:48Z). Line numbers refer to that commit.

## 1. Every place that assumes the client lives at the root

**packages/web**
| Where | What it assumes | Needs a change? |
|---|---|---|
| `vite.config.ts:6-18` | No `base`, so the default is `/`. `index.html` gets `/assets/index-*.js` as absolute URLs. The dev proxy covers `/api`, `/mcp`, `/auth`, `/ws` (`:11-14`). | **Yes**: add `base` (see §2). The proxy can stay as it is. |
| `index.html:10` | `<script type="module" src="/src/main.tsx">` | No. Vite rewrites it to the base at build time. |
| `src/api.ts:314` (`HttpApi.call` → `fetch(path)`), every path is `"/api/…"` (`:334-378` and on) | API calls are absolute from the root | No. /api stays at the root. |
| `src/api.ts:446` | `${wss|ws}://${location.host}/ws` | No. /ws stays at the root. |
| `src/auth/auth.tsx:32` | `fetch("/api/auth/config")` | No. |
| `src/auth/auth.tsx:50` | `location.href = "/auth/github"` | No. /auth stays at the root. |
| `src/auth/auth.tsx:54` | `fetch("/auth/logout")` | No. |
| `src/auth/auth.tsx:55` | Sign out goes to `location.href = "/?guest"` | **Yes** → `${import.meta.env.BASE_URL}?guest` (or `/workshop/?guest`). |
| `src/auth/auth.tsx:42-46` | `?auth_error=` is read from `location.href` and works on any path | No. The server has to send it to /workshop/ instead (see server below). |
| `src/app.tsx:213` | After a token login: `location.href = "/"` | **Yes** → `import.meta.env.BASE_URL`. |
| `src/app.tsx:127` | `location.reload()` | No. It reloads the same path. |
| `src/route.ts:12-13, 35` | `docUrl`/`grantUrl` = `location.origin + location.pathname + #/doc\|grant/<id>`, and `replaceState(…location.pathname…)` | No. These already follow the path, so links become `/workshop/#/grant/<id>` without any change. |
| `src/panels/Places.tsx:165`, `src/panels/Markdown.tsx:64,75` | Use `grantUrl`/`docUrl` | No (same reason). |
| `src/panels/Markdown.tsx:105` | Bare ids become `<a href="dc_…">`, relative, and the click handler intercepts them | No. A middle-click opens `/workshop/dc_…`, and the SPA fallback has to cover that (see §2). |
| `src/panels/HowItWorks.tsx` | No hrefs or paths | No. |
| `src/mock/server.ts:32` | `?as=visitor` read from `location.search` | No. |
| `public/` | Does not exist. No root-absolute images: sprites are drawn in code and the favicon is a data: URI. | No. |
| `test/` | — | Add a small test for the BASE_URL redirects if you want, but it is optional. |

No string `href="/"` exists anywhere in `packages/web/src`.

**packages/server**
| Where | What it assumes | Needs a change? |
|---|---|---|
| `src/app.ts:23,30,78-79` | `DEFAULT_WEB_DIST` is served at `/` | **Yes**: serve it under the prefix. |
| `src/app.ts:82` | `fastifyStatic({ root: dist, wildcard: true })` with no prefix | **Yes** → `prefix: "/workshop/"` and `redirect: true`, so `/workshop` → `/workshop/`. |
| `src/app.ts:84-88` | `no-cache` on text/html | No. It also covers the homepage. |
| `src/app.ts:37` | `API_PREFIXES = ["/api","/ws","/mcp","/auth"]` | No. The list stays as it is. |
| `src/app.ts:90-97` | The SPA fallback serves `index.html` for **every** extension-less GET outside the API | **Yes**: only under `/workshop/`. Paths outside it should redirect to `/` (or return 404). |
| `src/auth/routes.ts:32` | `fail` redirects to `/?auth_error=…` | **Yes** → `/workshop/?auth_error=…` |
| `src/auth/routes.ts:43` | After the callback, redirect to `/` | **Yes** → `/workshop/` |
| `src/auth/github.ts:5,14` | `redirect_uri = ${publicUrl}/auth/github/callback` | No. The OAuth callback URL does not change. |
| `src/auth/session.ts:50,58,65` | Session cookie `Path=/`; state cookie `Path=/auth` | No. The cookie covers /workshop/ and /api alike. |
| `src/auth/config.ts:59` | `publicUrl` = `MUSTER_TOWN_PUBLIC_URL`, no path | No. It stays `https://muster.town`. |
| `test/auth.test.ts:86, 114` | Expect `location` `"/"` and `/^\/\?auth_error=/` | **Yes**: update both. |
| `test/helpers.ts:13`, `desk.test.ts:33`, `auth.test.ts:49` | Every test passes `webDist: false` | **No test covers static serving or the SPA fallback today.** Add one in PR 1 (see §2). |

**Everything else**
- `packages/legacy-web-alias/package.json:5`: just `npm run build --prefix ../web`. It has no path assumption, so nothing to change.
- Fly prod: `fly.town.toml:10-42`. It has no path rules: one `http_service` → 4322, and the health check is `/api/health`, which stays. `MUSTER_TOWN_PUBLIC_URL = "https://muster.town"` (`:17`) stays. `deploy/fly/Dockerfile:19` runs `npm run build`, which picks up the new base automatically. Nothing to change.
- `deploy/Caddyfile` (the old box): plain `reverse_proxy`, no paths. Nothing to change.
- Redeploy: `npm run build --workspace @muster-town/web` (`docs/architecture.md:120`, `deploy/bootstrap.sh:73`). Nothing to change.
- `README.md:31`: the OAuth app's *Homepage URL* is `http://localhost:4322` and the callback is `…/auth/github/callback`. The callback is unchanged. The Homepage URL is only cosmetic on GitHub's consent screen, so no change is needed. `README.md:36`: `MUSTER_TOWN_PUBLIC_URL` is unchanged. **Do edit** one sentence in the README to say the client is at `<url>/workshop/` and the homepage at `/`.
- `docs/architecture.md:94`: "Static: serves `packages/web/dist` at `/`". **Must change** (AGENTS.md standing rule 4).
- Agents' prompts and core: no web URLs are built in `packages/core|runtime|desk|cli` (grep finds no `#/doc`, `#/grant` or publicUrl). Nothing to change.

## 2. The smallest PR 1: client at /workshop/, /api, /ws and /auth stay at the root

1. **Vite base.** In `vite.config.ts`, set `base: process.env.MUSTER_TOWN_WEB_BASE ?? "/workshop/"`. *(Alternative: `base: "./"`. One build then works under any prefix, which is good for a future `/climate/`. But `/workshop` without the slash would then load `/assets/…` and break, so the trailing-slash redirect becomes required. I'd go with the explicit `/workshop/` now: it is simpler to reason about, and today one server runs one collective.)*
2. **Server static under a prefix.** In `app.ts:82`, use `fastifyStatic({ root: dist, prefix: WEB_BASE, wildcard: true, redirect: true })` with `WEB_BASE = "/workshop/"`. Make it a `BuildAppOptions.webBase`, defaulting to `"/workshop/"`, so tests can set it. Optionally derive it later from a `slug` in collective.json, defaulting to the collective dir's basename (`collectives/workshop` → `workshop`).
3. **SPA fallback (`app.ts:90-97`).** Serve `index.html` only when `path.startsWith(WEB_BASE)`. Any other extension-less GET outside the API redirects 302 to `/` (or returns 404). This keeps `/workshop/dc_…` (a middle-clicked relative id link) working.
4. **Old root links.** For PR 1, until the homepage exists: `app.get("/")` → `302 /workshop/` plus the original `?query`. The server never sees the `#/grant/x` part. **Browsers carry the fragment across a redirect whose Location has none** (RFC 9110 §10.2.2), so `muster.town/#/grant/x` → `/workshop/#/grant/x` with no extra code. PR 2 replaces this redirect with the homepage, so the homepage must then do the hash forwarding itself (see §3).
5. **Post-login redirect.** `auth/routes.ts:43` → `redirect(WEB_BASE)`. `:32` → `` `${WEB_BASE}?auth_error=…` ``. Web: `auth.tsx:55` and `app.tsx:213` use `import.meta.env.BASE_URL`.
6. **Tests.**
   - Update `auth.test.ts:86,114`.
   - Add an `app.test.ts` that builds with a temp `webDist` (an `index.html` plus `assets/x.js`) and asserts:
     - `GET /` → 302 `/workshop/`
     - `GET /workshop` → 301/302 `/workshop/`
     - `GET /workshop/` → index.html with `no-cache`
     - `GET /workshop/assets/x.js` → 200
     - `GET /assets/x.js` → 404
     - `GET /workshop/#…` style deep path `/workshop/foo` → index.html
     - `GET /api/health` is unchanged
     - a missing `/workshop/assets/y.js` → 404 JSON, not HTML
7. **Docs.** `docs/architecture.md:94`, one README sentence, and a line in `docs/log.md`.

Estimated size: about 6 files changed, ~25 lines of code plus ~40 lines of test. /api, /ws, /mcp, /auth, the cookies and the OAuth app all stay untouched.

**Dev loop**
- Vite dev: `npm run dev --workspace @muster-town/web` on :5173. With `base: "/workshop/"`, Vite serves the app at `http://localhost:5173/workshop/`. A bare `/` there shows Vite's "did you mean /workshop/" hint, which is fine. The proxy (`vite.config.ts:11-14`) is unchanged, because /api, /auth and /ws are still at the root of the target.
- Mock without a backend: `VITE_MOCK=1 npx vite` in `packages/web` → `localhost:5173/workshop/` (`?as=visitor` for a visitor).
- To test the server routes in practice (homepage, redirects): run `npm run build --workspace @muster-town/web`, then `npm run dev` (server :4321, `MUSTER_TOWN_DEV=1`), then open `:4321/` and `:4321/workshop/`.
- Screenshots: `/home/agent/tools` **does not exist on my desk**, and my old `/tmp/pr55tool/cdp.mjs` is gone (the /tmp folder was wiped). `/usr/bin/chromium` is installed. `chromium --headless=new --no-sandbox --virtual-time-budget=8000 --window-size=1400,900 --screenshot=/tmp/x.png <url>` is enough for the homepage and for `/workshop/#/grant/<id>`.

## 3. The homepage at /

**Options**
- (a) A second Vite entry (multi-page `rollupOptions.input`): it is built and hashed like the app, but it adds build config and a second dev URL just to show a list.
- (b) **Static HTML the server renders from a collectives list.**
- (c) The same SPA with a route: every stranger would download the map bundle (`chunkSizeWarningLimit: 900` kB) and boot the town's WebSocket just to read a list. It also ties a page that lists *many* collectives to one collective's client.

**Recommendation: (b).** Put a new `packages/server/src/home.ts`:
- `collectives(world)` returns the list.
- `renderHome(list)` returns one self-contained HTML string with inline CSS in the town's palette (`#14151c`, `#7cc4ff`).
- Register `app.get("/")` (sent `no-cache` by the existing hook) and `app.get("/api/collectives")` returning the same list.

Why (b):
- No build step.
- The list renders without JS, so it is fast and crawlable for strangers.
- The API and the page come from one source.
- It works the same in prod and dev.
- It is about 80 lines plus a test.

The only JS the homepage needs is a 2-line inline script that forwards old links: `if (/^#\/(doc|grant)\//.test(location.hash)) location.replace("/workshop/" + location.hash)`. Run it before render so an old `muster.town/#/grant/x` link never shows the homepage.

**List shape** (zod in `packages/schema`):
```
Collective = { slug: string, name: string, tagline: string, goal: string, url: string, placeholder?: true }
```
- **Workshop entry:** built live from the town row (`GET /api/town` already returns `name` "Workshop Collective", `goal`, `tagline`). It uses slug `workshop` and url `/workshop/`, so name and goal edits show up without a deploy.
- **Placeholder entries:** a small checked-in list, e.g. `collectives/registry.json` `[{slug:"next", name:"Your collective here", tagline:"…", goal:"…", url:"", placeholder:true}]`. Load it at startup with schema validation, and fall back to empty if it's missing.
- A placeholder renders as a card labelled "Coming soon" with no Open link (the grant says: not a dead link), plus a line on how to start one, e.g. a link to the repo README.
- The Workshop card shows name, tagline, goal and an **Open** button → `/workshop/`.

## 4. What I could not determine from the code (check live)

1. **Fragment preservation through the PR 1 `/` → `/workshop/` 302 on real browsers**, especially in-app browsers such as Slack/GitHub previews. The spec and major browsers say yes. Check: open `https://muster.town/#/grant/gr_jqsqra0dlx` in a private window and expect `/workshop/#/grant/gr_jqsqra0dlx` with the grant panel open.
2. **Today `/workshop` already returns 200** (live, 15:48Z), because the SPA fallback serves `index.html` for any path. So before the PR, a 200 at /workshop proves nothing. After the PR, check that the bundle URL in `/workshop/` is `/workshop/assets/index-*.js` and that `/assets/…` 404s.
3. **Open tabs during the deploy.** A tab open at `/` with the old bundle reconnects after the redeploy. If it reloads (`app.tsx:127`), it lands on `/` → the redirect, or in PR 2 the homepage. That's harmless, but Mitchell's open tab will jump once.
4. **GitHub OAuth app settings**: I can't see them from here. The callback URL does not change, so nothing should need editing. Check: one real sign-in after PR 1 lands on `/workshop/` with the session still valid. Mitchell's existing 30-day cookie (`Path=/`) should survive, since nothing about the cookie changes.
5. **External links that use a root path other than a hash**, e.g. somebody linking `muster.town/?guest`. None exist in the repo. After PR 1 they still reach the client via the query-preserving redirect. After PR 2, `?guest` on the homepage is ignored, which is acceptable.
6. Whether any local collective (e.g. `start:climate`) needs a different base. Locally, everything will also live at `/workshop/` unless `MUSTER_TOWN_WEB_BASE` is set. That is fine for now; say so in the README.

