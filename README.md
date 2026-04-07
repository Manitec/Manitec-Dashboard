# Manitec Projects KB

> Empire HQ for everything Joe builds, breaks, and ships.

[![Deploy MkDocs](https://github.com/Manitec/Manitec-Dashboard/actions/workflows/deploy.yml/badge.svg)](https://github.com/Manitec/Manitec-Dashboard/actions/workflows/deploy.yml)

**Live site:** [info.manitec.pw](https://info.manitec.pw)

---

## What This Is

A [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) knowledge base documenting the Manitec empire — infrastructure, projects, philosophy, and dev logs.

Automatic deploys to GitHub Pages on every push to `main`.

## Structure

```
docs/
  blog/          → Dev logs & posts
  infra/         → Infrastructure docs (Cloudflare, Render, Vercel, DashNex)
  projects/      → Project pages (ManiBot, HexBot, Ebbinor, Banjoshire...)
  philosophy/    → Counterthism & coding philosophy
  hexbot/        → HexBot-specific docs
  css/           → Custom cyberpunk theme
meta/
  generate_task_fragments.py   → Auto-generates task status from GitHub Issues
.github/workflows/
  deploy.yml     → Auto-deploy on push to main (with pip caching)
```

## Local Dev

```bash
pip install -r requirements.txt
mkdocs serve
# → http://127.0.0.1:8000
```

## Deploy

Push to `main` — GitHub Actions handles the rest.
Or trigger manually from the [Actions tab](https://github.com/Manitec/Manitec-Dashboard/actions).

---

*Manitec Future (LLC) — Own your stack. Own your data. Own your destiny.*
