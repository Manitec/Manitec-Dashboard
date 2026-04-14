# Manitec Control Hub

**What it is:** Joe's private ops dashboard — a password-gated Next.js app for monitoring deployments, managing services, and running empire infrastructure from one interface.

## Stack

- **Framework:** Next.js 15 (App Router)
- **Hosting:** Vercel
- **Auth:** Middleware password gate — `httpOnly` cookie, `HUB_DASHBOARD_PASSWORD` env var
- **Backend:** Proxies to Manitec Command Hub (FastAPI) for deploy actions

## Features (Live ✅)

- Password gate — middleware-level, redirects unauthorized requests to `/login`
- Deploy status view — recent deployment visibility with redeploy action
- Mail admin quick access
- Dark cyberpunk UI — neon cyan/purple on near-black

## Next Steps

- [ ] Route all deploy actions through Command Hub as the single backend authority
- [ ] Add service health indicators per project
- [ ] Add GitHub activity feed
- [ ] Replace shared password gate with stronger token/session auth

## Lessons Learned

- Next.js 15 — `useSearchParams()` must be wrapped in a `<Suspense>` boundary or build fails at static generation
- `httpOnly` cookies can't be read by JS — keep auth logic server-side only
