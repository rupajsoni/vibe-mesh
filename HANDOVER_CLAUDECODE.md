# Claude Code Handover — Vibe Mesh

## Read this before doing anything

Read all four documents in this order before writing a single line:

1. `CLAUDE.md` — project spec, axes, moods, rules, what is blocked
2. `FOUNDATION.md` — product philosophy and mission. Understand what we are building and why.
3. `ARCHITECTURE.md` — system design, stack, dependency flow
4. `DECISIONS.md` — open technical decisions. Do not assume answers to anything listed here.

Then confirm you have read all four by summarizing: what the project is, what phase it is in, what the two things that block implementation are, and what is missing from the scaffold.

Do not write any code until I confirm your summary is correct.

---

## What exists

The scaffold is in place. These files exist but contain no logic:

```
cmd/api/main.go
internal/gateway/spotify.go
internal/handlers/query.go
internal/models/song.go
internal/platform/config.go
internal/platform/server.go
internal/repository/vector_repo.go
internal/service/vibe_service.go
data/seeds.json
```

One file is missing from the scaffold and needs to be created:
- `internal/gateway/clap.go` — the CLAP client. Decided as part of architecture. Not yet created.

---

## What is locked and ready to implement

- 6 axes: Energy, Groove, Production (name TBD — see below), Vocals, Emotion, Social
- All normalized 0.0–1.0
- 10 mood presets with vectors — all in CLAUDE.md
- Discover mode — expand search radius + nudge 1–2 axes by delta. ~10 lines. In MVP.
- Dependency flow: handlers → service → repository + gateway → models. Strict. Do not break.
- Uber Fx for all wiring. No manual constructors in main.go.

---

## What blocks implementation — resolve before writing code

**1. Production axis name**
The sixth axis concept is locked. The word is not. It blocks every struct field that references it. Candidates: Texture, Grain, Edge, Grit. Ask me to pick one before touching models.

**2. Axis → CLAP query translation**
How do 6 float values become a semantically rich CLAP text prompt? This is the soul of the product. It has not been designed. Do not invent it. Flag it when you reach service logic and wait.

**3. Router**
net/http or Chi. Not decided. Flag when writing server.go. Default to net/http unless I say otherwise.

---

## Rules for this session

- `go build ./...` after every file. Do not let build errors accumulate.
- Read each existing file before writing to it. Do not assume it is empty.
- Explicit over clever. Every function readable without context.
- If something in CLAUDE.md is ambiguous, ask. Do not assume.
- Keep functions small. One thing per function.
- Start with `internal/models/song.go`. Get the data types right first. Everything flows from them.

---

## Where to start when I say go

`internal/models/song.go` — define the core structs:
- `VibeVector` — 6 fields, one per axis (Production field name TBD — resolve first)
- `Song` — ID, title, artist, vector, metadata
- `MoodPreset` — name, dimension, vector
- `Query` — the incoming request shape
- `QueryResult` — the outgoing response shape

Get these right. The rest of the codebase is downstream of them.
