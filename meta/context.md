## Manitec / Joe context snapshot

- I’m Joe in East Tennessee — solo builder, philosopher/tinkerer. My company is **Manitec Future LLC**.
- Main brand domain: **manitec.pw** (served via DashNex).
- Personal hub: **joesfaves.com** (projects, experiments, personal stuff).
- Other key endpoints:
  - Docs KB: https://manitec.github.io/Manitec-Dashboard/
  - Custom webmail: https://mail.manitec.pw/ (FastAPI app, “Manitec Mail” using Zoho Mail360 + SQLite users.db)
  - AI chat: https://chat.manitec.pw (ManiBot / Hexbot)
  - Voxel world: https://ebbinor.joesfaves.com (Minetest)

### Infra stack

- DNS/CDN: **Cloudflare**
- Apps platform: **DashNex** (~22 apps, landing pages, funnels, etc.)
- Backend hosting: **Render** (FastAPI services, e.g., Manitec Mail)
- Email API: **Zoho Mail360**
- Docs system: **MkDocs** repo `Manitec-Dashboard` with:
  - `docs/infra/*` for infrastructure
  - `docs/projects/*` for individual projects
  - `docs/philosophy/*` for philosophy / Counterthism

### Manitec Mail (mail.manitec.pw)

- Repo: https://github.com/Manitec/mailserver
- Tech: FastAPI + SQLite + Zoho Mail360 API.
- `users.db` (or `DB_PATH`) has table `users(id, username, password_hash, account_key, from_address)`.
- Passwords are SHA256 hex hashes (Python hashlib), used consistently in both CLI init script and FastAPI app.
- There is a CLI (`init_users.py`) to init DB, add users, and list users.
- Admin is currently hard-coded as `user.id == 2` for `/admin` operations.
- `users.db` is treated as **secret** and kept *out* of GitHub; only schema and code live in the repo.

### DashNex usage & design system

- DashNex is the front-of-house layer for:
  - manitec.pw (brand)
  - parts of joesfaves.com (personal hub)
- It’s used only for marketing/landing/static-ish stuff, no secrets/databases.
- Design system (for DashNex-safe pages):
  - Background: `#07070f`
  - Purple accent: `#9b30ff`
  - Cyan accent: `#00f5ff`
  - Fonts: Space Grotesk (UI) + JetBrains Mono (code)
  - Bootstrap 4.1.3
  - Heroes use `<img>` (no CSS background-image)
  - Button groups use:

    ```css
    .mn-btn-group {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
    }
    ```

- In `Manitec-Dashboard` under `docs/infra/`, there are:
  - `dashnex-system-summary.md` (how DashNex fits into the stack)
  - `dashnex-page-build-checklist.md` (step-by-step checklist for new pages)
  - `mkdocs.yml` has both wired into the “Infrastructure” nav.

### Current status / priorities

- `/my-projects/` on joesfaves.com:
  - Structure and text are done; needs images/screenshots per project.
- Docs that still need love:
  - `docs/philosophy/index.md` (missing)
  - `docs/infra/index.md` (basically empty intro)
- Goals:
  - Consistent DashNex pages using the design system + checklist.
  - A proper **Banjoshire** landing page.
  - Better-organized project/docs pages that can grow into business assets.

### How to use this file

- Use this as a quick boot-up context for new tools/assistants.
- It should stay roughly accurate even as projects evolve; update when infra or core URLs change.
