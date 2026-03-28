# Infrastructure Overview

Manitec Future (llc) runs lean, mean, and sovereign. No Big Cloud lock-in — just battle-tested tools stacked for maximum tinker-control.

## The Stack
Cloudflare (DNS/CDN)
↓ ├── DashNex (marketing/landings)
├── Render (FastAPI backends like Manitec Mail)
├── MkDocs (this docs site)
└── Zoho Mail360 (email API)

- **Public-facing**: DashNex for cyberpunk pages (manitec.pw, joesfaves.com).
- **Dynamic**: Render hosts FastAPI services (e.g., mail.manitec.pw with SQLite users.db).
- **Knowledge**: This MkDocs repo — `infra/`, `projects/`, `philosophy/`.

Detailed breakdowns: [DashNex System](dashnex-system-summary.md).

[Philosophy](../philosophy/) | [Projects](../projects/)
