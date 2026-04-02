# everytriv-link

Static **GitHub Pages** site that sends visitors to your **public frontend URL** (read from `frontend-target.json`). Default target is the [EveryTriv](https://github.com/IsraelRub/EveryTriv) source repo until you set a **tunnel URL** for the Docker client (port 3000).

Keep EveryTriv secrets out of this repo.

## Files

| File | Role |
|------|------|
| `index.html` | Loads `frontend-target.json` and redirects (HTTPS URLs only). |
| `frontend-target.json` | `{ "frontendUrl": "https://..." }` — your public SPA URL (`CLIENT_URL`). |

## One-time setup

1. Create a **public** GitHub repository named `everytriv-link` (or use [IsraelRub/everytriv-link](https://github.com/IsraelRub/everytriv-link)).
2. Put `index.html` and `frontend-target.json` in the repo root.
3. **Pages**: Repository → **Settings** → **Pages** → **Deploy from a branch** → `main`, folder **`/` (root)**.
4. Stable link: **https://israelrub.github.io/everytriv-link/**

## Playable demo (tunnel)

1. Run EveryTriv with Docker; expose **3000** (SPA) and **3002** (API) via two tunnels.
2. Set root `.env` in EveryTriv: `CLIENT_URL`, `SERVER_URL`, `VITE_API_BASE_URL`; rebuild client if needed.
3. Set `frontendUrl` in `frontend-target.json` to the **HTTPS** frontend tunnel URL; commit and push.

Or from the monorepo:

`scripts/deployment/sync-demo-redirect.ps1 -ApiTunnelUrl ... -FrontendTunnelUrl ... -EverytrivLinkRepoPath "<path>" -GitPush`

## Google OAuth (if used)

- **Authorized JavaScript origins**: `CLIENT_URL`
- **Authorized redirect URIs**: `{SERVER_URL}/auth/google/callback`

## Validation

From EveryTriv: `scripts/deployment/validate-demo-redirect.ps1` with your Pages URL and expected `CLIENT_URL`.
