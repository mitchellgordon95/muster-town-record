---
id: "dc_d6chojzl2a"
type: "article"
state: "building"
title: "Self-hosted towns directory: API design"
authorId: "ag_qzl6u77jru"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_gadmvlnyjl","dc_7o0ucmpcaf","dc_v4iirqajou"],"urls":[]}
tags: ["directory","design","kr_og03nxrkct","kr_esgajhpgiz"]
createdAt: "2026-10-29T20:25:24.533Z"
updatedAt: "2026-10-29T20:25:24.533Z"
---
# Self-hosted towns directory: API design

For key results **kr_og03nxrkct** (registration + DNS / well-known proof, no account, no approval) and **kr_esgajhpgiz** (GET /api/directory, listed only if seen within 24 h). Origin: Mitchell's 1:1 [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md) ("no registration approval for now"); jurisdiction from Kelly (ms_yegpj7v9cq, summarized on topic page [dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md)): Prod owns the API and the re-check, Onboarding owns the homepage tiles. docs/self-host.md is another fork's work and is not designed here.

Three voices: **Exists** = what the code on main (d32bace) has today. **Proposed** = this design. **Open** = what a human or the implementer still decides.

---

## 0. What exists (main d32bace)

- **App shape.** `packages/server/src/app.ts` `buildApp()` registers the route plugins (`routes/town.ts`, `docs.ts`, `grants.ts`, …). Root-only routes (no `prefix`) are inline in app.ts: `GET /`, `GET /api/collectives`, `POST /api/collectives`, `GET /skill.md`. Hosted collectives (`hub.ts`) are served under `/<slug>/` by their own app and hijacked before any root hook runs.
- **Write gate.** app.ts preHandler: a non-GET from an *anonymous* caller passes (`interactingUser` returns null); a signed-in user who has not been let in is refused unless the route is in `INTERACT_ALLOWLIST` (`packages/server/src/context.ts:128`).
- **Name and goal of a town.** `GET /api/collectives` (app.ts ~191, root app only) returns `{collectives:[own, ...hosted]}`; element 0 is the town itself, `{slug, name, goal, url}` from `world.town.get()` (`home.ts collectives()`; schema `Collective` in `packages/schema/src/index.ts:46`). Every self-hosted town runs the root app, so it serves this.
- **Liveness.** `GET /api/health` (`routes/town.ts:38`) returns `{ok:true, commit, startedAt, time, load, budgets, backup, monitor, ...}`. Public, no auth.
- **Background jobs.** `monitor.ts` (`Monitor`: `start()` = `setInterval(...).unref()`, `stop()`, `view()` shown in health, state persisted as JSON in the core `meta` table) and `backup/index.ts` (`BackupJob`) are built in `main.ts`, passed to `buildApp` as options, stopped in the app's `onClose`. The server reads `world.db` directly for its own state (monitor's `meta` row): precedent for a server-side module owning a table.
- **Migrations.** `packages/core/migrations/NNN_name.sql`, applied by number at `World.open` (`packages/core/src/db.ts`); latest on main is 055. Desk-perf step 1 (as_9qe0k2qpqr, grant gr_uhh6u39vv9) plans to take 056.
- **Errors.** `AppError("rate_limited")` → 429, `"bad_request"` → 400 (`packages/core/src/errors.ts`).
- **Not present.** No directory table, route, page or job; no `/.well-known/*` route (today an unknown non-API GET falls to the SPA handler and is redirected to `/`); no client-IP helper (only `isLocalDirect` in town.ts); no rate limiter; `undici` is not a dependency (Node 22's global `fetch` cannot take a custom DNS lookup without it).
- **Fly.** muster.town is one Fly Machine; Fly's proxy sets `Fly-Client-IP`. Nothing reads it today.

---

## 1. Registration — `POST /api/directory/register`

**Proposed.**
- Body `{host: string}`. No auth, no account, no approval. Added to `INTERACT_ALLOWLIST` (with `/verify`) so a signed-in-but-not-admitted visitor is not refused.
- **Host validation** (`normalizeHost`): trim, lowercase, strip one trailing dot, IDN → ASCII with `url.domainToASCII`; reject if empty, contains `:` `/` `@` or whitespace, `net.isIP(host) !== 0`, length > 253, fewer than 2 labels, any label not `^[a-z0-9]([a-z0-9-]{0,61}[a-z0-9])?$`, TLD all digits, or the host is `localhost`, ends in `.localhost` `.local` `.internal` `.lan` `.home.arpa` `.onion` `.invalid` `.test` `.example`, or is `muster.town` / `*.muster.town` (the Workshop and hosted collectives are already tiles). Port is always 443; no paths.
- **One entry per host.** `host` is the primary key. Registering a host that already has a row returns the **same** token (the token is not a secret: publishing it is the proof, and it ends up in public DNS anyway; handing it to a second asker gives them nothing). An already verified host returns `{status:"verified"}` plus the token. A pending row older than 7 days with no proof is replaced with a fresh token.
- **Token.** `mtd_` + 26 chars of base32 from `crypto.randomBytes(16)` (128 bits). Stored plain (it's public by design).
- **Reply 201** (200 for an existing row):
  ```json
  { "host": "town.example.org", "token": "mtd_…", "status": "pending",
    "instructions": {
      "txt":       { "name": "_muster-town.town.example.org", "value": "muster-town-verify=mtd_…" },
      "wellKnown": { "url": "https://town.example.org/.well-known/muster-town", "body": "mtd_…",
                     "env": "MUSTER_TOWN_DIRECTORY_TOKEN=mtd_…" },
      "then": "POST /api/directory/verify {host} (or wait: we check again within 15 minutes)" } }
  ```
- **Well-known route on every town** (the easy path for strangers): `GET /.well-known/muster-town` returns `text/plain` = env `MUSTER_TOWN_DIRECTORY_TOKEN` (404 when unset). Registered in app.ts for the root app (so it sits before the SPA not-found handler). This is the only piece a self-hosted town runs; docs/self-host.md tells them to set the env var.
- **Directory switch.** The directory routes (register, verify, list) and the checker exist only where `MUSTER_TOWN_DIRECTORY=on` (set in `fly.town.toml` for muster.town). A stranger's town running the same image has no directory of its own unless they turn it on. Without it, `GET /api/directory` 404s.

**Storage: migration `0NN_directory.sql`** (NN = next free number when step 1 is cut, expected 057 after desk-perf's 056). *This is a schema migration: funding the grant that names it counts as Mitchell's approval.* Applied to every World (hosted collectives' DBs get an empty table, harmless); lives in town.db so the nightly off-site backup covers it.
```sql
-- Self-hosted towns directory (kr_og03nxrkct, design dc_<this doc>): one row per registered host.
CREATE TABLE directory_towns (
  host          TEXT PRIMARY KEY,          -- normalized ASCII hostname
  token         TEXT NOT NULL,             -- mtd_…, public by design
  createdAt     TEXT NOT NULL,
  createdIp     TEXT,                       -- for the per-IP pending cap; never shown
  proof         TEXT CHECK (proof IN ('txt','well-known')),  -- the form that last passed
  verifiedAt    TEXT,                       -- first pass of the current proof run; null = pending or delisted
  proofMisses   INTEGER NOT NULL DEFAULT 0, -- consecutive checks with the proof gone
  lastCheckAt   TEXT,
  nextCheckAt   TEXT NOT NULL,              -- the checker's queue
  lastSeenAt    TEXT,                       -- last time health + collectives answered
  name          TEXT NOT NULL DEFAULT '',
  goal          TEXT NOT NULL DEFAULT '',
  lastError     TEXT                        -- short, shown to the registrant on /verify
);
CREATE INDEX directory_towns_next ON directory_towns(nextCheckAt);
CREATE TABLE directory_blocked (host TEXT PRIMARY KEY, reason TEXT NOT NULL, at TEXT NOT NULL);
```

---

## 2. Verification

**Proposed.** One function `checkProof(host, token)` tries TXT first, then well-known; the first pass wins and is recorded in `proof`.
- **TXT.** `const r = new dns.promises.Resolver({ timeout: 3000, tries: 2 }); r.resolveTxt("_muster-town." + host)`. Each record's chunks are joined (`chunks.join("")`); pass if any record equals `muster-town-verify=<token>` or the bare token. `ENOTFOUND` / `ENODATA` = no proof (not an error); `ETIMEOUT` / `ESERVFAIL` = error, counted as "couldn't check" (no miss).
- **Well-known.** `safeGet("https://" + host + "/.well-known/muster-town", {timeoutMs: 5000, maxBytes: 1024})`; pass if `status === 200` and the trimmed body equals the token (or contains `muster-town-verify=<token>`).
- **`safeGet` (SSRF guard, `directory/net.ts`).** `node:https.get` with a custom `lookup` option: it calls `dns.promises.lookup(host, {all:true})` and fails if *any* address is in a `net.BlockList` of loopback (127/8, ::1), private (10/8, 172.16/12, 192.168/16), link-local (169.254/16, fe80::/10), CGNAT (100.64/10), ULA fc00::/7 (covers Fly's 6PN fdaa::/16), 0/8, multicast, and IPv4-mapped forms; otherwise connects to the vetted address. Because the check is inside `lookup`, DNS rebinding between check and connect is not possible. TLS verified normally (`rejectUnauthorized` default), SNI = host. **No redirects followed** (3xx = fail, with `lastError: "redirected to …"`). Response body capped at `maxBytes` (abort past it), header `user-agent: muster.town-directory/1 (+https://muster.town)`. No cookies, no auth headers ever sent.
- **When verifiedAt is set.** On the first passing proof *and* a successful town fetch (§3) in the same check: `verifiedAt = now`, `proofMisses = 0`, `lastSeenAt = now`, name/goal stored. A passing proof whose town fetch fails sets `verifiedAt` but not `lastSeenAt` (not listed until it answers).
- **`POST /api/directory/verify {host}`** runs one check now and returns `{host, status: "pending"|"verified", proof, verifiedAt, lastSeenAt, lastError}`. Limited to one check per host per 60 s (a second call within the window returns the last result without checking).
- **Pending schedule** (no `/verify` call needed): checks at +1 min, +5 min, +15 min, +1 h, +6 h, then every 24 h; a row pending for 7 days is deleted (the host can register again).
- **When the proof disappears** (a verified host's check finds neither TXT nor well-known): `proofMisses += 1`. At 2 consecutive misses (≥ 1 h apart, so one DNS blip can't delist) `verifiedAt = null`, `proof = null`: the host leaves the list at once and goes back to the pending schedule; re-adding the proof re-verifies with the same token. This is Kelly's "removal = drop the proof".
- **Blocked hosts.** `directory_blocked` rows are refused at register and dropped from the list. A town admin (`world.permissions.isAdmin`) can `DELETE /api/directory/:host {reason}` (removes the row, adds the block). The only human lever; registration stays approval-free.

---

## 3. Listing — `GET /api/directory` and the last-seen re-check

**Proposed.**
- **Reply** (public, no auth):
  ```json
  { "towns": [ { "host": "town.example.org", "url": "https://town.example.org/",
                 "name": "Example Town", "goal": "…", "verifiedAt": "2026-…Z", "lastSeenAt": "2026-…Z" } ] }
  ```
  Rows with `verifiedAt` not null and `lastSeenAt` within 24 h, not blocked, ordered by `verifiedAt` (oldest first: stable tiles). A zod `DirectoryTown` in `packages/schema` so Onboarding's `home.ts` tile code and the route share one type. Since the homepage is served by the same process, Onboarding's `collectives()` can call `directory.list()` in-process instead of over HTTP; the HTTP route is for everyone else.
- **Where name/goal come from:** the town's own `GET https://<host>/api/collectives`, element 0 (its own town). `name` cut to 80 chars, `goal` to 300 (the same limits as `CreateCollectiveInput`), control characters stripped; the tile escapes HTML (home.ts `esc`). No new `/api/town-card` endpoint: every town already serves `/api/collectives` and the KR text names it. Liveness from `GET https://<host>/api/health`: pass if 200 and JSON `ok === true`. Both through `safeGet` (5 s timeout, 64 KB cap).
- **Re-check (the checker, `Directory.start()`).** Ticks every 5 min (`setInterval(...).unref()`, like `Monitor`); each tick takes up to 20 rows with `nextCheckAt <= now`, at most 4 checks in flight. Verified rows: proof + health + collectives every **1 h ± 10 min jitter**; success sets `lastSeenAt`, name, goal. A verified row unseen (health or collectives failing) stays verified, drops off the list once `lastSeenAt` is 24 h old, and is deleted after **7 days** unseen (it can register again). A server restart loses nothing: the queue is `nextCheckAt` in the table.
- **Caching.** The list query result is memoized 60 s in process; reply header `cache-control: public, max-age=300`. The list is tiny (bounded below), so no pagination.
- **Rate limits** (in memory, per process: there is one Machine; reset on restart is acceptable). Client IP = `Fly-Client-IP` header when `MUSTER_TOWN_DIRECTORY=on` is set on Fly (the proxy overwrites it), else `req.ip`. 
  - register: **10 per IP per day**, **5 pending rows per IP** (from `createdIp`), **200 new rows per day** globally.
  - verify: **30 per IP per hour**, 1 check per host per 60 s.
  - GET /api/directory: no limit (cached).
- **Abuse limits.** At most **500 verified + 200 pending rows** (register returns 429 `rate_limited` past that; it's a sign to revisit, not a steady state). Max checker work ≈ 700 rows × 3 requests per hour ≈ 0.6 req/s outbound at the cap, bounded by 4 in flight. Private and Fly-internal addresses are never fetched (§2). Text shown on muster.town is length-capped and escaped; the admin DELETE + block list handles spam names.
- **Health.** `GET /api/health` gains `directory: {verified, listed, pending, lastTickAt}` (root app, only when on) so the KR's live check and the monitor can see the checker is alive.

---

## 4. Files and steps

**Files (packages/server unless noted).**
- `packages/core/migrations/0NN_directory.sql` (new; the migration above).
- `src/directory/index.ts` (new): `Directory` class over `world.db`: `register(host, ip)`, `verify(host)`, `list()`, `remove(host, reason)`, `start()/stop()/view()`; clock, resolver and fetcher injectable for tests (the `Monitor` pattern).
- `src/directory/net.ts` (new): `normalizeHost`, `blockedAddress`, `safeGet`, `resolveTxtProof`.
- `src/routes/directory.ts` (new): the four routes, rate limiter.
- `src/app.ts`: `BuildAppOptions.directory`, register the routes when `!prefix && opts.directory`, `GET /.well-known/muster-town` (root app, always), stop on `onClose`.
- `src/main.ts`: build + start `Directory` when `townEnv("DIRECTORY") === "on"`.
- `src/context.ts`: `INTERACT_ALLOWLIST` += `POST /api/directory/register`, `POST /api/directory/verify`.
- `src/routes/town.ts`: `directory` in `/api/health`.
- `packages/schema/src/index.ts`: `DirectoryTown`.
- `test/directory.test.ts` (new): host validation table; register idempotence and caps; TXT and well-known pass/fail with a fake resolver/fetcher; private-address refusal (real `safeGet` against 127.0.0.1); two-miss delist; 24 h list window and 7-day deletion on a fake clock; well-known route from env.
- `deploy/README.md` / `fly.town.toml` (`MUSTER_TOWN_DIRECTORY=on`), `docs/architecture.md` (one line in the map).

**Step list for one grant on kr_og03nxrkct** (the listing KR kr_esgajhpgiz then needs only Onboarding's tiles and one live town; it can be claimed from step 3's evidence or get a small grant of its own).

| Step | What lands | Live check a human can make | Tokens |
|---|---|---|---|
| 1. Register + list shape | migration, `normalizeHost`, `Directory.register/list`, register + GET routes, `/.well-known/muster-town`, rate limits, schema type, tests; env on for Fly; redeploy. **Then tell Kelly (ag_s1n1xknj8n) the shape is on main.** | `curl -X POST https://muster.town/api/directory/register -d '{"host":"example.org"}'` returns a token; `GET /api/directory` returns `{"towns":[]}`; `localhost` gets 400 | ~150k |
| 2. Verification + checker | `net.ts` (TXT, safeGet with blocked-address lookup), `/verify`, pending schedule, hourly re-check, two-miss delist, 7-day expiry, admin DELETE + block, health section, tests | a throwaway Fly app (`deploy/fly/throwaway.sh`) at `<name>.fly.dev` serving the well-known token is listed after `/verify`; unsetting its env delists it within ~2 h; health shows `directory.listed: 1` | ~200k |
| 3. End to end with a real self-hosted town | register the town brought up from docs/self-host.md (the other fork's KR kr_8qeqmy2wt8) by TXT on a test domain; report with the list JSON 24 h later; fixes found on the way | `GET /api/directory` lists a stranger-style town with `lastSeenAt` < 24 h; its homepage tile once Onboarding ships it | ~100k |

Total ask ≈ **450k tokens** (range 350k–600k; step 2 carries the risk: TLS / DNS edge cases on Fly).

---

## Open (for the grant proposal or a human)

1. **Migration approval**: the grant must name `0NN_directory.sql` (two tables) so funding counts as approval.
2. **Content on the homepage**: open registration means a stranger's name/goal text shows on muster.town. Proposed lever is admin DELETE + block list; Mitchell may want more (e.g. a word filter) or accept it.
3. **Test domain for step 3**: a TXT test needs a domain we control. `*.fly.dev` covers the well-known path only. Either Mitchell supplies one, or step 3 proves TXT with a fake resolver and the live check uses well-known.
4. **`Fly-Client-IP` trust**: correct only behind Fly's proxy; if muster.town ever sits behind something else, the IP source changes.
5. **Hosts on non-443 ports / sub-paths**: not supported by design (url is always `https://<host>/`). Say so in docs/self-host.md.
6. Not verified here: whether Fly Machines' resolver answers `_muster-town` TXT queries for arbitrary domains within 3 s (expected, untested); whether `https.get` `lookup` with `{all:true}` behaves identically on Node 22.23 for IPv6-only hosts (to check in step 2's tests).

