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

## Full flow (tunnel install, `.env`, rebuild, OAuth, checks)

EveryTriv monorepo **`README.md`** → **«דמו ציבורי — טונל אחד»** (Docker).  
Technical reference for **cloudflared** (CLI + Docker Compose profile): **`docs/deployment/CLOUDFLARED.md`** in that repo.

## Google OAuth (if used)

- **JavaScript origins** and **redirect** `…/auth/google/callback`: same `https://` host as the tunnel (single-tunnel).
