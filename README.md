# Vibes Mesh

> *Search music right from the heart.*

A music discovery frontend that replaces search with feeling. Describe how you want music to feel across six science-backed dimensions — the sliders and radar chart send that to a Go backend, which cosine-matches against pre-vectorized songs and returns ranked results. No popularity bias, no genre filter.

**This is `vibe-mesh` (public)** — frontend only: `index.html`, `index-beta.html`, `living-brief.html`, `curator-deck.html`, `company-north-star.html`. The Go backend and all strategy/process docs live in a separate **private** sibling repo, [`vibe-mesh-core`](https://github.com/rupajsoni/vibe-mesh-core) — that's where `CLAUDE.md`, `TASKS.md`, and everything else you'd expect in a project root actually is.

---

## Live

- **[vibesmesh.netlify.app](https://vibesmesh.netlify.app)** — the canonical/professional link.
- **[rupajsoni.github.io/vibe-mesh](https://rupajsoni.github.io/vibe-mesh)** — casual mirror, same product.

## Local development

No build step — plain HTML/CSS/JS. Serve with any static server on a CORS-allowlisted port:

```bash
python3 -m http.server 3000
```

Open `http://localhost:3000/index.html`. It talks to `http://localhost:8080` automatically (the backend from `vibe-mesh-core` needs to be running there — see that repo's README). Override the target with `?api=https://your-api.com`.

## Deploying

See `DEPLOYMENT.md` for the full breakdown. Short version: GitHub Pages deploys straight from `main`, ungated. Netlify deploys from a separate `production` branch — pushing to `main` only builds a preview at `main--vibesmesh.netlify.app`; promote with `git push origin main:production` once it looks right.

---

Built by [@rupajsoni](https://github.com/rupajsoni)
