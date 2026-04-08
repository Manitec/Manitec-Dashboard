# Why MkDocs Snippets Silently Ate My Content (and How to Fix It)

*April 7, 2026 &middot; Joe &middot; Tutorial &middot; ~6 min read*

> Also published at [manitec.pw/blog/mkdocs-snippets](https://manitec.pw/blog/mkdocs-snippets/)

---

Here’s a fun way to waste an afternoon: build an automated system that generates markdown files in CI, include them in your docs with `pymdownx.snippets`, deploy successfully, and then discover that every single page is completely blank where your content should be.

No errors. No warnings. Just… nothing.

This happened to me while building the [Manitec Dashboard](https://info.manitec.pw) — a MkDocs site that auto-pulls GitHub Issues and renders them as live task lists. The CI pipeline ran fine. The deploy succeeded. The pages were empty.

Here’s exactly why it happens and how to fix it in two lines.

---

## What is `pymdownx.snippets`?

The `pymdownx.snippets` extension lets you include the contents of one file inside another using a special syntax:

```markdown
--8<-- "path/to/file.md"
```

It’s incredibly useful for:

- Auto-generated content (task lists, changelogs, status pages)
- Reusable content blocks shared across multiple pages
- CI-generated markdown injected into docs at build time

When it works, it’s magic. When it doesn’t, it fails silently — which makes debugging it particularly painful.

---

## The Problem: Path Resolution

Here’s the thing nobody tells you upfront.

`pymdownx.snippets` resolves include paths **relative to the `docs/` directory by default**. Not the repo root. Not where `mkdocs.yml` lives. The `docs/` directory.

So if your generated files live at `meta/tasks/tasks-hexbot.md` in the repo root, and your page includes:

```markdown
--8<-- "meta/tasks/tasks-hexbot.md"
```

Snippets looks for that file at `docs/meta/tasks/tasks-hexbot.md` — which doesn’t exist. Instead of throwing an error, it silently produces… nothing. The include is just removed. Your page renders empty and MkDocs doesn’t say a word about it.

This is the behavior. It’s documented, technically — but buried, and the silent failure makes it extremely hard to diagnose.

---

## The Fix: `base_path`

The `pymdownx.snippets` extension accepts a `base_path` configuration option that tells it where to look for included files. You can pass multiple paths and it searches them in order.

In your `mkdocs.yml`:

```yaml
markdown_extensions:
  - pymdownx.snippets:
      base_path:
        - .       # repo root
        - docs    # docs directory (default behavior preserved)
```

That’s it. Two lines. Adding `.` (the repo root) to `base_path` means snippets can now find files anywhere in your repository, not just inside `docs/`.

---

## Full Working Setup

Here’s the complete pattern for CI-generated snippets that actually work:

### 1. Generate your files in CI

```yaml
# .github/workflows/deploy.yml
jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      - run: pip install mkdocs-material
      - run: python meta/generate_fragments.py   # runs BEFORE deploy
      - run: mkdocs gh-deploy --force
```

!!! warning "Order matters"
    Your generation script **must run before** `mkdocs gh-deploy`. If you run them in the wrong order, MkDocs builds before the files exist and you get the same silent empty output.

### 2. Write defensively in your generator

If your script calls an external API (like GitHub Issues), handle failures gracefully:

```python
def fetch_issues(slug):
    resp = requests.get(f"{API_URL}/{slug}/issues", headers=HEADERS)
    
    if resp.status_code == 404:
        print(f"INFO: repo not found for '{slug}' — writing empty snippet.")
        return []
    if resp.status_code == 403:
        print(f"INFO: 403 for '{slug}' — writing empty snippet.")
        return []
    
    resp.raise_for_status()
    return resp.json()
```

Without this, a missing repo or expired token crashes the entire deploy pipeline.

### 3. Configure `base_path` in `mkdocs.yml`

```yaml
markdown_extensions:
  - pymdownx.snippets:
      base_path:
        - .
        - docs
```

### 4. Use the include in your markdown

```markdown
## Open Tasks

--8<-- "meta/tasks/tasks-hexbot.md"
```

---

## Why Silent Failure?

The silent behavior is intentional — snippets is designed to be used in contexts where optional includes are valid. But it means you need to verify your output actually contains content after a deploy, not just that the build succeeded.

A quick sanity check: after deploying, view the page source or inspect the rendered HTML. If your `--8<--` include produced nothing, the path is wrong.

---

## Quick Reference

| Symptom | Cause | Fix |
|---|---|---|
| Page renders empty where snippet should be | Wrong path resolution | Add `base_path: [., docs]` to snippets config |
| CI crashes during deploy | Generator script fails on API error | Add 404/403 guards, return empty list |
| Custom domain reverts after deploy | No `CNAME` in `docs/` | Create `docs/CNAME` with your domain |
| Snippet works locally, fails in CI | File not generated before build | Move generator script before `mkdocs gh-deploy` |

---

## TL;DR

If your `--8<--` includes are producing blank output with no errors:

1. Add `base_path: [., docs]` to your `pymdownx.snippets` config
2. Make sure your generator runs *before* `mkdocs gh-deploy` in CI
3. Add graceful error handling so API failures don’t nuke your deploy

The fix is two lines. The diagnosis is the hard part.

---

*Built by Joe — [Manitec.pw](https://manitec.pw)*

[Back to Blog](index.md) | [Home](../index.md)
