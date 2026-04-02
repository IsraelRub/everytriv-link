# everytriv-link

Static **GitHub Pages** site that redirects visitors to your current **public frontend URL** (tunnel to EveryTriv Docker client on port 3000).

Copy this folder to a **separate** GitHub repository named `everytriv-link` (or push only these files there). Keep EveryTriv secrets out of this repo.

## One-time setup (plan steps 1–5)

1. Create a new **public** GitHub repository named `everytriv-link`.
2. Add `index.html` from this folder to the repo root. Replace every `REPLACE_ME_FRONTEND_TUNNEL` with your real frontend tunnel URL (must start with `https://`).
3. Enable **Pages**: Repository → **Settings** → **Pages** → Build and deployment → **Deploy from a branch** → branch `main` (or `master`), folder **`/` (root)**.
4. After the first deployment, your stable link will look like:
   - `https://<github-username>.github.io/everytriv-link/`
   - or `https://<org>.github.io/everytriv-link/` for an organization.
5. Share only that Pages URL; update `index.html` whenever your **frontend** tunnel URL changes (see EveryTriv `scripts/deployment/`).

## EveryTriv reminder

- You need **two** public URLs for Docker demo: **frontend** (port 3000) and **API** (port 3002). The redirect page only points to the frontend.
- Set root `.env` in EveryTriv: `CLIENT_URL`, `SERVER_URL`, and `VITE_API_BASE_URL` (same as public API base as `SERVER_URL` for typical setups).
- Rebuild the **client** image after changing `VITE_API_BASE_URL`: `docker compose build client` from the EveryTriv repo root.

## Google OAuth (if used)

After URL changes, update Google Cloud Console:

- **Authorized JavaScript origins**: your `CLIENT_URL`
- **Authorized redirect URIs**: `{SERVER_URL}/auth/google/callback`

## Validation checklist (after each tunnel change)

1. Open the GitHub Pages URL → should redirect to the SPA.
2. SPA loads; API calls succeed (check network tab).
3. Multiplayer: WebSocket connects if you test it.
4. Google sign-in completes without redirect errors (if enabled).

## Automation

From the EveryTriv monorepo, use `scripts/deployment/sync-demo-redirect.ps1` to update root `.env`, optionally rebuild Docker client, and refresh `index.html` in a local clone of this repo.
