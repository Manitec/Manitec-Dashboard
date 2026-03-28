# Infrastructure Overview

Manitec Future (LLC) runs lean, mean, and sovereign. No Big Cloud lock-in — just battle-tested tools stacked for maximum tinker-control.

## The Stack

```
Cloudflare (DNS/CDN)
  ├── DashNex (marketing/landings → manitec.pw, joesfaves.com)
  ├── Render (FastAPI backends → mail.manitec.pw, chat.manitec.pw)
  ├── GitHub Pages (this docs site → manitec.github.io)
  └── Zoho Mail360 (email API)
```

## Services

| Category | Service | URL | Purpose |
|----------|---------|-----|---------|
| Domain | manitec.pw | [manitec.pw](https://manitec.pw) | Primary domain |
| Mail | Custom Webmail | [mail.manitec.pw](https://mail.manitec.pw) | Self-hosted inbox |
| Backend | Render | [render.com](https://render.com) | FastAPI host |
| Apps | DashNex | [dashnex.com](https://dashnex.com) | 22 app pages |
| Email API | Zoho Mail360 | [mail360.zoho.com](https://mail360.zoho.com) | Transactional mail |
| DNS/CDN | Cloudflare | [cloudflare.com](https://cloudflare.com) | Speed + security |
| Chat | HexBot | [chat.manitec.pw](https://chat.manitec.pw) | AI chat interface |

!!! warning "Action Items"
    - Regenerate Firebase Admin SDK key (see env var CSV).
    - Push dashnex-system-summary to DashNex page.
    - Apply cyberpunk CSS to manitec.pw.

## Detailed Docs
- [Tools & Services](./tools.md)
- [DashNex System Summary](./dashnex-system-summary.md)
- [DashNex Page Build Checklist](./dashnex-page-build-checklist.md)
- [Oracle Cloud](./oracle-cloud.md)
- [GenX Router API](./genx-router.md)

[Philosophy](../philosophy/) | [Projects](../projects/)
