# FiveM & Cfx.re API Documentation

Unofficial reference for Cfx.re, FiveM, RedM, and FXServer HTTP endpoints.  
**Last Updated:** November 4, 2026

> [!NOTE]
> Cfx.re frequently updates or migrates its internal infrastructure. If you find an endpoint that no longer works, does not exist anymore, or is missing from this documentation, please open a **Pull Request** or submit an **Issue**.

> [!IMPORTANT]
> Cfx.re migrated the server list API from `servers-frontend.fivem.net` to `frontend.cfx-services.net` and `gss.cfx-services.net`. Requests to the legacy `servers-frontend.fivem.net/api/servers/single/{id}` endpoint now return `404 Not Found`.

---

## 1. Server Browser & Master List API

These endpoints power the official FiveM and RedM server browser UI (`servers.fivem.net`).

| Resource | Method | Endpoint | Notes |
| :--- | :--- | :--- | :--- |
| **Single Server Info** | `GET` | `https://frontend.cfx-services.net/api/servers/single/{joinId}` | Replace `{joinId}` with the Cfx.re join code (e.g., `rmmblap`). |
| **All Servers Stream** | `GET` | `https://frontend.cfx-services.net/api/servers/streamRedir/` | Trailing slash required. `302` redirects to `/api/servers/stream/{unixTimestamp}/` (Protobuf binary stream). |
| **Server Icon** | `GET` | `https://frontend.cfx-services.net/api/servers/icon/{joinId}/{iconVersion}.png` | `iconVersion` is returned inside the Single Server JSON payload. |
| **Featured Servers (FiveM)** | `GET` | `https://gss.cfx-services.net/v1/public/featured-servers/fivem` | Replaces the legacy `/api/servers/top/{language}` endpoint. |
| **Featured Servers (RedM)** | `GET` | `https://gss.cfx-services.net/v1/public/featured-servers/redm` | Featured/spotlight RedM servers. |
| **Community Tweets** | `GET` | `https://gss.cfx-services.net/v1/public/tweets` | Replaces the legacy `runtime.fivem.net/tweets.json` endpoint. |
| **Pinned Servers** | `GET` | `https://runtime.fivem.net/pins.json` | Global pinned server configuration. |
| **Promotions Targeting** | `GET` | `https://runtime.fivem.net/promotions_targeting.json` | Promotion targeting rules. |
| **Server Upvote** | `GET` | `https://frontend.cfx-services.net/api/upvote/` | Requires valid Cfx session/entitlement headers (returns `403` unauthenticated). |

> [!TIP]
> When querying `frontend.cfx-services.net/api/servers/single/{joinId}` from a script or bot, include a standard browser `User-Agent` header.

---

## 2. Direct FXServer Instance API

Every running FXServer exposes local HTTP endpoints on its game port.

| Resource | Method | Endpoint | Description |
| :--- | :--- | :--- | :--- |
| **Server Info** | `GET` | `http://{ip}:{port}/info.json` | Static server metadata, convars, resources list, and icon version. |
| **Dynamic Status** | `GET` | `http://{ip}:{port}/dynamic.json` | Current player count (`clients`), `sv_maxclients`, hostname, and mapname. |
| **Player List** | `GET` | `http://{ip}:{port}/players.json` | Connected players, server IDs, pings, and public identifiers. |

> [!WARNING]
> Many public servers enable `sv_httpFloodProtection` or hide player endpoints (`sv_endpointPrivacy`), causing direct requests to `/players.json` or `/dynamic.json` to time out or return `403`. Use `https://frontend.cfx-services.net/api/servers/single/{joinId}` for reliable status polling without exposing server IPs.

---

## 3. Runtime, Natives, Artifacts & Platform Status

Endpoints used by the FiveM/RedM client runtime, build updaters, and status monitors.

### Player Counts & Runtime Config

| Resource | Method | Endpoint |
| :--- | :--- | :--- |
| **Global Counts (Legacy Runtime)** | `GET` | `https://runtime.fivem.net/counts.json` |
| **FiveM Player Counts** | `GET` | `https://static.cfx.re/runtime/counts.json` |
| **RedM Player Counts** | `GET` | `https://static.cfx.re/runtime/counts_rdr3.json` |
| **NUI Blacklist** | `GET` | `https://runtime.fivem.net/nui-blacklist.json` |
| **Pool Size Limits (FiveM)** | `GET` | `https://content.cfx.re/mirrors/client/pool-size-limits/fivem.json` |
| **Pool Size Limits (RedM)** | `GET` | `https://content.cfx.re/mirrors/client/pool-size-limits/redm.json` |
| **Policy User Info** | `GET` | `https://policy-live.fivem.net/api/getUserInfo/{id}` |
| **Cfx.re Platform Status** | `GET` | `https://status.cfx.re/api/v2/summary.json` |

### Artifacts, Changelogs & Natives

| Resource | Method | Endpoint |
| :--- | :--- | :--- |
| **Windows Server Artifacts** | `GET` | `https://changelogs-live.fivem.net/api/changelog/versions/win32/server` |
| **Linux Server Artifacts** | `GET` | `https://changelogs-live.fivem.net/api/changelog/versions/linux/server` |
| **Specific Build Changelog** | `GET` | `https://changelogs-live.fivem.net/api/changelog/versions/{win32\|linux}/server/{buildversion}` |
| **Client Artifacts Index** | `GET` | `https://runtime.fivem.net/artifacts/fivem/` |
| **FiveM Natives (Lua)** | `GET` | `https://static.cfx.re/natives/natives.lua` |
| **RedM Natives (Lua)** | `GET` | `https://static.cfx.re/natives/natives_rdr3.lua` |

---

## 4. Forum & User Account API (`forum.cfx.re`)

The Cfx.re forum runs on Discourse and exposes standard Discourse JSON endpoints.

| Resource | Method | Endpoint | Auth Required |
| :--- | :--- | :--- | :--- |
| **User Profile** | `GET` | `https://forum.cfx.re/u/{username}.json` | No |
| **Username Availability** | `GET` | `https://forum.cfx.re/u/check_username.json?username={username}` | No |
| **Email Availability** | `GET` | `https://forum.cfx.re/u/check_email.json?email={email}` | Yes (Session) |
| **Current Session** | `GET` | `https://forum.cfx.re/session/current.json` | Yes (Cookie) |
| **CSRF Token** | `GET` | `https://forum.cfx.re/session/csrf.json` | Yes (Cookie) |
| **Send Activation Email** | `POST` | `https://forum.cfx.re/u/action/send_activation_email` | Yes (CSRF + Ticket) |

### Example: `POST /u/action/send_activation_email`

**Headers:**
```json
{
  "Cfx-Entitlement-Ticket": "<ownership_ticket>",
  "X-Requested-With": "XMLHttpRequest",
  "Discourse-Present": "true",
  "X-CSRF-Token": "<csrf_token>",
  "Content-Type": "application/x-www-form-urlencoded"
}
```

**Body (Form Data):**
```ini
username=<your_username>
```

---

## 5. Deprecated & Removed Endpoints

> [!CAUTION]
> The following endpoints from older FiveM API documentation are offline, restricted, or have been permanently replaced. Do not use them in new projects.

| Legacy Endpoint | Status | Replacement / Reason |
| :--- | :--- | :--- |
| `https://servers-frontend.fivem.net/api/servers/single/{address}` | `404 Not Found` | Replaced by `https://frontend.cfx-services.net/api/servers/single/{joinId}` |
| `https://servers-frontend.fivem.net/api/servers/streamRedir` | `404 Not Found` | Replaced by `https://frontend.cfx-services.net/api/servers/streamRedir/` |
| `https://servers-frontend.fivem.net/api/servers/top/{language}` | `404 Not Found` | Replaced by `https://gss.cfx-services.net/v1/public/featured-servers/fivem` |
| `https://runtime.fivem.net/tweets.json` | `404 Not Found` | Replaced by `https://gss.cfx-services.net/v1/public/tweets` |
| `https://changelogs-live.fivem.net/api/changelog/versions/{build}` | `404 Not Found` | Requires OS/target path: `/api/changelog/versions/{win32\|linux}/server/{build}` |
| `https://lambda.fivem.net/api/ticket/playtimes/{ip:port}?identifiers[]={id}` | `503 Unavailable` | Decommissioned; no public replacement. |
| `https://lambda.fivem.net` | `403 / 503` | Internal CnL service; blocked from public access. |
| `https://cnl-hb-live.fivem.net` | `Unreachable` | Legacy CnL heartbeat endpoint; offline. |
| `https://sentry.fivem.net/auth/login` | `Unreachable` | Internal Sentry instance; offline. |
| `https://runtime.fivem.net/loadscreen/spotlight-2/WebGL-GTA` | `Obsolete` | Legacy client loadscreen asset. |

---

## Contributing

If any endpoint listed in this documentation is outdated, broken, or missing, please open a **Pull Request** with the updated URL and details.
