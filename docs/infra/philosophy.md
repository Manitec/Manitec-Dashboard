# Manitec Global Development Philosophy

## Rule #1 — Free Until Forced

Never pay for infrastructure unless a free solution is technically impossible or would severely compromise the product. Always exhaust free tiers first.

### Approved Paid Exceptions

| Service | Cost | Justification |
|---|---|---|
| DashNex | Pay-per-use credits, no subscription | Blog, 22 apps, GenX Router API — too useful to avoid |
| Shopify store | ~$6/month | E-commerce, no free equivalent |
| Domain names | Variable | Unavoidable — you own your identity |

## Rule #2 — Repo as CDN

Static assets that never change (default avatars, UI images, option sets) live in the repo and get served via Vercel's CDN — not Firebase Storage. Firebase Storage is for user-generated content only.

## Rule #3 — No Subscriptions If Possible

Even when paying, prefer pay-as-you-go over locked monthly fees. DashNex credits model is the ideal pattern — spend only when you're actually creating something.

## Free Stack in Use

| Service | Purpose |
|---|---|
| Vercel | Hosting / deployment |
| Firebase | Auth, Firestore, Storage |
| Neon | Serverless Postgres |
| Groq API | AI inference |
| Cloudflare | DNS / CDN |
| GitHub | Repos / version control |
| DashNex | Blog / site management |
| Render | FastAPI backend |
| Zoho/Mail360 | Email API |
| Oracle Cloud | VPS / game server |
