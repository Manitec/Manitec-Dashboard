# Banjoshire

**Origin:** Built for Joe's son who wanted a Discord-style hangout site for him and his friends. They never really used it — but building it reignited Joe's passion for coding, web dev, and app development. Banjoshire is the reason Manitec exists.

**Live URL:** [banjo.joesfaves.com](https://banjo.joesfaves.com)

**NOT Appalachian themed.** Just a name.

## Stack

- **Framework:** Next.js (deployed on Vercel)
- **Backend/DB:** Firebase (project ID: `banjoshire`)
- **Auth:** Firebase Auth
- **Storage:** Firebase Storage (custom user assets) + repo-hosted static assets (default avatars, banners)

## Features (Working ✅)

- User login / auth
- Channels
- Real-time messaging
- User profile cards — banner image, circular avatar, username + discriminator tag, member since date, online/offline indicator, message button

## Storage Philosophy

Default avatar/banner options are served from the repo via Vercel CDN — not Firebase Storage. Firebase Storage is reserved for user-uploaded custom assets only. Keeps costs at zero.

## Status

Core complete. Taking a break. Next feature: fully wire user-selectable avatars/banners from repo-hosted options.

## Next Steps

- [ ] Wire user-selectable default avatars from repo
- [ ] Wire user-selectable banners from repo
- [ ] User profiles — bio, status message
- [ ] Roles and permissions
- [ ] Friends list / follow system
