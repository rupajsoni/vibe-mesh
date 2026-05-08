# Deployment Guide

## Local Development

```bash
go run ./cmd/api
```

The UI will be served at `http://localhost:8080` and will automatically use the local backend.

## GitHub Pages Deployment

### Setup (one-time)

1. Push code to GitHub (includes `.github/workflows/deploy.yml`)
2. Go to your repo: **Settings → Pages**
3. Under "Build and deployment":
   - Source: **Deploy from a branch**
   - Branch: **gh-pages** / **(root)**
4. GitHub Actions will automatically deploy the latest main branch

### Access the deployed UI

- **index.html (v1)**: `https://rupajsoni.github.io/vibe-mesh/`
- **index-v2.html (v2)**: `https://rupajsoni.github.io/vibe-mesh/index-v2.html`

### Connect to a backend API

The UI defaults to `http://localhost:8080` but you can override it:

```
https://rupajsoni.github.io/vibe-mesh/?api=https://your-api.com
```

This is useful when your backend is deployed separately (e.g., on Heroku, Cloud Run, etc.).

## Backend Deployment

The Go backend can be deployed independently:

```bash
# Build binary
go build -o vibe-mesh ./cmd/api

# Run on port 8080
PORT=8080 SEEDS_PATH=data/seeds.json ./vibe-mesh
```

Then access the deployed UI with:
```
https://rupajsoni.github.io/vibe-mesh/?api=https://your-deployed-backend.com
```
