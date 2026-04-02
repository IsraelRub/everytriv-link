# everytriv-link

Static **GitHub Pages** site: redirects to your **public HTTPS** tunnel (Docker client port **3000**). The tunnel URL lives **only** in `index.html` (`FRONTEND_DEMO_URL`). Local play: open `http://localhost:3000` on the machine that runs Docker — not this site.

Keep EveryTriv secrets out of this repo.

## Files

| File | Role |
|------|------|
| `index.html` | Sets `var FRONTEND_DEMO_URL = "https://…";` then redirects (public HTTPS only; empty = show setup text). |

## One-time setup

1. Public GitHub repository (e.g. [IsraelRub/everytriv-link](https://github.com/IsraelRub/everytriv-link)).
2. Put `index.html` in the repo root.
3. **Pages**: Settings → **Pages** → branch `main`, folder **`/`**.
4. Stable entry: **https://israelrub.github.io/everytriv-link/** (until `FRONTEND_DEMO_URL` is set, visitors see instructions).

## Playable demo

1. EveryTriv: `docker compose up`.
2. HTTPS tunnel to `http://127.0.0.1:3000`.
3. Monorepo `.env`: `SERVER_URL` + `CLIENT_URL` = tunnel; `VITE_API_BASE_URL=USE_ORIGIN_API_PREFIX`; rebuild client if needed.
4. In this repo: set `FRONTEND_DEMO_URL` in `index.html` to the same `https://…` and push — or from monorepo:

`scripts/deployment/sync-demo-redirect.ps1 -FrontendTunnelUrl 'https://…' -EverytrivLinkRepoPath "<clone>" -GitPush`

**Two tunnels (legacy):** `-ApiTunnelUrl` + `-FrontendTunnelUrl`; set `VITE_API_BASE_URL` to the API tunnel in `.env`.

## Google OAuth (if used)

- **JavaScript origins** and **redirect** `…/auth/google/callback`: same `https://` host as the tunnel (single-tunnel).

## Validation

From EveryTriv monorepo:

- `scripts/deployment/verify-demo-remote.ps1 -TunnelBaseUrl 'https://…' -PagesUrl 'https://…github.io/everytriv-link'`
- `scripts/deployment/validate-demo-redirect.ps1`
