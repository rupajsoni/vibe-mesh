# Deployment Guide

This repo is frontend-only (`index.html` and friends) — there is no backend here anymore. The Go API lives in the private sibling repo, [`vibe-mesh-core`](https://github.com/rupajsoni/vibe-mesh-core), deployed separately on Render. See that repo's README for backend setup/deploy.

## Local development

Serve this repo with any static file server, on a CORS-allowlisted origin (`localhost:8080`, `:3000`, or `:3001`):

```bash
python3 -m http.server 3000
```

Then open `http://localhost:3000/index.html`. `API_BASE` in `index.html` auto-detects `localhost`/`127.0.0.1` and points at `http://localhost:8080` (where the backend from `vibe-mesh-core` should be running). Override with `?api=https://your-api.com` if pointing at something else.

## GitHub Pages

Deploys automatically from `main` via `.github/workflows/deploy.yml` — no manual setup needed, this is already configured. Live at `https://rupajsoni.github.io/vibe-mesh/`. Ungated by design — this is the casual/friends-and-family mirror, not the professional link.

## Netlify

Deploys from the `production` branch, **not** `main` — this is deliberately gated (see `vibe-mesh-core`'s `docs/process/deploy-strategy.md` for the full model). Live at `https://vibesmesh.netlify.app` — this is the canonical/professional link.

- Push to `main` → builds a preview at `main--vibesmesh.netlify.app`. Check it there first.
- When it looks right: `git push origin main:production` — that's what actually updates the live site.

## Connecting to a different backend

Any deployed frontend page accepts a `?api=` override:

```
https://vibesmesh.netlify.app/?api=https://your-api.example.com
```

Useful for pointing a deployed frontend at a local or staging backend temporarily.
