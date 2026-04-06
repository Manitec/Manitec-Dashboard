# How I Accidentally Broke My Docs Site 6 Ways and Fixed Them All in One Afternoon

*April 6, 2026 · Joe · Dev Log + Tutorial · ~8 min read*

> Also published at [manitec.pw/blog/docs-fixes](https://manitec.pw/blog/docs-fixes)

---

There’s a certain kind of programmer satisfaction that comes not from building something shiny, but from systematically destroying and then resurrecting your own infrastructure in a single sitting. Today was that day.

My docs site — [info.manitec.pw](https://info.manitec.pw) — is built with MkDocs Material and deployed to GitHub Pages via a CI workflow. It’s been “working” for weeks. Except it wasn’t really working. It was *appearing* to work while quietly accumulating problems like a storage unit nobody opens.

Here’s every bug, why it happened, and how I killed it.

---

## Bug #1: Task Snippets Were Silently Empty

I built a system where each project page auto-pulls open GitHub Issues from a private tasks repo and renders them as a live task list using `pymdownx.snippets`. The Python script ran in CI, wrote the markdown files, everything looked fine.

Except the pages were blank. No errors — just empty sections where tasks should be.

**Why:** `pymdownx.snippets` resolves `--8<--` include paths relative to the `docs/` directory by default. My generated files lived at `meta/tasks/` — the repo root — which snippets had no idea about.

**Fix:**
```yaml
# mkdocs.yml
- pymdownx.snippets:
    base_path:
      - .       # repo root
      - docs    # docs directory
```

Two lines. Thirty minutes of confusion. Classic.

---

## Bug #2: CI Would Nuke Itself if the Tasks Repo Didn’t Exist

The task-generation script called the GitHub API for a private repo (`Manitec-Tasks`). If that repo didn’t exist — or the token lacked the right permissions — the script threw an unhandled exception and crashed the entire deploy pipeline.

Two problems hiding in one:

**Problem A:** The workflow only had `contents: write` permission. The Issues API needs `issues: read`.

```yaml
# .github/workflows/deploy.yml
permissions:
  contents: write
  issues: read   # ← this was missing
```

**Problem B:** No graceful fallback. A 404 or 403 from the API was a hard crash instead of writing an empty snippet.

```python
if resp.status_code == 404:
    print(f"INFO: repo not found for '{slug}' — writing empty snippet.")
    return []
if resp.status_code == 403:
    print(f"INFO: 403 for '{slug}' — writing empty snippet.")
    return []
```

Now if the tasks repo isn’t ready, the build keeps going and renders “No open tasks” instead of dying.

---

## Bug #3: The Theme Was Fighting My Own CSS

`mkdocs.yml` had `primary: deep purple` and `accent: indigo` from Material’s built-in palette. My custom `cyberpunk.css` was simultaneously trying to override everything with neon cyan, purple, and pink. Two systems wrestling in the cascade and neither was fully winning.

Fix: give up on Material’s palette colors entirely and let the CSS own the aesthetics.

```yaml
theme:
  palette:
    - scheme: slate
      primary: black
      accent: cyan
```

Neutral base. Custom CSS takes it from there. No more cascade wars.

---

## Bug #4: Neon Glows Rendering Against the Wrong Background

The cyberpunk neon effects looked great in my head. In the browser they looked washed-out because the page background was Material’s default dark slate instead of the true near-black (`#0a0a0f`) I wanted.

The `--dark-bg` CSS variable was defined but never applied to the actual page surfaces. Defining a variable and *using* it are two different things.

```css
.md-main,
.md-header,
.md-tabs,
.md-sidebar,
[data-md-color-scheme="slate"] {
  --md-default-bg-color: #0a0a0f;
  background-color: #0a0a0f;
}
```

The neon glows properly now.

---

## Bug #5: Custom Domain Reverting to github.io on Every Deploy

This one bites a lot of MkDocs users. I had `info.manitec.pw` set as a custom domain in GitHub Pages settings. After every deploy it reverted back to `manitec.github.io/Manitec-Dashboard/`.

**Why:** `mkdocs gh-deploy` rebuilds the `gh-pages` branch from scratch on every run. GitHub Pages reads the custom domain from a `CNAME` file in the branch root. If that file isn’t in your source `docs/` folder, it gets wiped on every deploy.

**Fix — two parts:**

1. Create `docs/CNAME` containing just your domain:
```
info.manitec.pw
```
MkDocs copies everything in `docs/` into the built site, so this file survives every deploy forever.

2. Update `site_url` in `mkdocs.yml`:
```yaml
site_url: https://info.manitec.pw/
```

!!! tip "Cloudflare DNS"
    Point `info` → `manitec.github.io` as a CNAME with the proxy **off** (grey cloud).
    GitHub Pages handles HTTPS itself — proxying through Cloudflare at the same time causes certificate conflicts.

---

## Bug #6: Stale URLs and a Dead Nav Link

A full docs audit turned up three quiet wrongnesses:

- **HexBot** listed with `chat.manitec.pw` — that’s ManiBot’s URL. HexBot lives at `hex.manitec.pw`.
- **ManiBot** listed with stack “Python” — it’s Next.js 15, Vercel AI SDK, Groq, and Neon.
- A **Chatbot** row in the projects table linked to `projects/chatbot.md` — a file that doesn’t exist. Silent 404.

None of these broke the build. They just made the docs quietly wrong, which is somehow worse.

---

## The Lesson

Docs sites feel low-stakes until they’re the thing you hand someone when they ask “where can I learn about your projects?” These fixes took one afternoon but the bugs had been silently accumulating for weeks. An occasional audit — even just reading your own docs top-to-bottom — catches a surprising amount.

The full Manitec empire docs live at **[info.manitec.pw](https://info.manitec.pw)** — now actually working as intended.

---

*Built in East Tennessee. Broken and fixed in the same afternoon. 🤖*

---

[Back to Blog](index.md) | [Home](../index.md)
