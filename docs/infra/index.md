# Infrastructure Overview

![Manitec Infrastructure](https://i.postimg.cc/PrpdhTdT/dx_Ox_S0v_Jq7p_Wzb2ONT2X_0_CM_M5.jpg)

Manitec Future (LLC) runs lean, mean, and sovereign. No Big Cloud lock-in — just battle-tested tools stacked for maximum tinker-control.

## The Stack

```
Cloudflare (DNS/CDN)
  ├── DashNex (marketing/landings → manitec.pw, joesfaves.com)
  ├── Render (FastAPI backends → mail.manitec.pw, hex.manitec.pw)
  ├── Vercel (Next.js apps → chat.manitec.pw, banjo.joesfaves.com, dash.manitec.pw)
  ├── GitHub Pages (docs → manitec.github.io)
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
| Chat | HexBot | [hex.manitec.pw](https://hex.manitec.pw) | AI chat interface |
| Chat | ManiBot | [chat.manitec.pw](https://chat.manitec.pw) | Personal AI assistant |
| Dashboard | Control Hub | [dash.manitec.pw](https://dash.manitec.pw) | Empire command center |

!!! warning "Action Items"
    - Regenerate Firebase Admin SDK key (see env var CSV).
    - Deploy Control Hub to Vercel → dash.manitec.pw.
    - Apply cyberpunk CSS to manitec.pw.

## Detailed Docs
- [Tools & Services](./tools.md)
- [DashNex System Summary](./dashnex-system-summary.md)
- [DashNex Page Build Checklist](./dashnex-page-build-checklist.md)
- [Oracle Cloud](./oracle-cloud.md)
- [GenX Router API](./genx-router.md)

[Philosophy](../philosophy/) | [Projects](../projects/)
