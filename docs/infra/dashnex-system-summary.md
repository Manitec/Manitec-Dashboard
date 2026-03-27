# Manitec DashNex System Summary

This document explains how DashNex fits into the Manitec Future stack, how the sites are wired, and the conventions to follow when building or updating DashNex pages.

---

## 1. High-level architecture

Manitec Future uses a small set of core services:

- **Primary domain:** `manitec.pw` – main public-facing brand domain.
- **Custom webmail:** `https://mail.manitec.pw/` – Manitec Mail (FastAPI + Zoho Mail360 API).
- **Web backend hosting:** Render.com – hosts the FastAPI mail client and any future Python backends.
- **Apps platform:** DashNex.com – manages multiple marketing / landing / utility apps (currently ~22).
- **Email API:** Zoho Mail360 – used as the backend mail provider for Manitec Mail.
- **DNS/CDN:** Cloudflare – front door for DNS, SSL, caching, and routing to DashNex, Render, and other services.

DashNex is used specifically as the **“marketing / site builder layer”** on top of this infra. It does not send email directly or handle custom APIs; instead, it consumes DNS mappings (via Cloudflare) and embeds / links out to backends where needed.

---

## 2. DashNex’s role in the stack

DashNex is the no-code / low-code layer for:

- Landing pages and funnels for Manitec Future properties.
- Content sites like **manitec.pw** and **joesfaves.com** (where appropriate).
- Simple forms and lead capture / opt-ins.
- Hosting static-content-style pages that need quick iteration.

### Key characteristics

- **DNS:** Cloudflare CNAMEs or records point subdomains to DashNex app endpoints.
- **Branding:** DashNex pages must follow the Manitec design system (see below).
- **Integration:** Any “real” functionality (authentication, dynamic data, AI tools, custom mail client) lives on FastAPI backends or other services and is linked or embedded from DashNex.

---

## 3. Current primary DashNex-connected sites

### 3.1 manitec.pw (primary brand domain)

- Hosted via DashNex (front-end experience).
- Represents Manitec Future LLC as the main cyberpunk-flavored brand hub.
- Used as the canonical domain in DNS and in copy.

### 3.2 joesfaves.com (personal hub)

- Personal brand / experiments / project directory.
- Uses DashNex (and/or embedded HTML) as the front-end presentation layer.
- Ties into:
  - **ebbinor.joesfaves.com** (Minetest voxel world).
  - **chat.manitec.pw** (AI/Hexbot front-end).
  - GitHub-hosted docs at `manitec.github.io/Manitec-Dashboard`.

---

## 4. Design system for DashNex pages

All DashNex pages for Manitec/Manibot/Hexbot should follow this shared design language:

- **Background color:** `#07070f`
- **Accent color (purple):** `#9b30ff`
- **Accent color (cyan):** `#00f5ff`
- **Typography:**
  - Primary: **Space Grotesk**
  - Code/mono: **JetBrains Mono**
- **Framework:** Bootstrap 4.1.3 recommended.
- **Hero images:** Use `<img>` tags; avoid `background-image` for heroes to keep DashNex-safe.
- **Buttons:**
  - Use flex group wrapper:

    ```css
    .mn-btn-group {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
    }
    ```

  - Keep primary CTA consistent across pages (e.g., “Launch App”, “Enter Banjoshire”, “Open Hexbot Chat”).

Consistency across DashNex and non-DashNex pages makes the system feel like one unified cyberpunk product family.

---

## 5. Content conventions

When building or updating a DashNex page:

1. **URL strategy**
   - Brand-level: `manitec.pw/...`
   - Personal / experimental: `joesfaves.com/...`
   - Avoid random slug chaos – use short, meaningful paths (e.g., `/banjoshire`, `/hexbot`, `/projects`).

2. **Navigation**
   - Ensure top-level links always include:
     - Home (brand or personal)
     - Projects / Apps
     - Contact / Support

3. **Integration links**
   - For apps with separate backends:
     - Link `mail.manitec.pw` for webmail.
     - Link `chat.manitec.pw` for AI/Hexbot.
     - Link docs at `https://manitec.github.io/Manitec-Dashboard/` for technical / dev info.

4. **Copy & tone**
   - Slightly playful, cyberpunk, helpful, not corporate.
   - Keep headings short, direct, and scannable.

---

## 6. Operational notes

- **Where DashNex fits:** It should remain the “front-of-house” for marketing and simple sites, not the place where you store secrets, user databases, or heavy backend logic.
- **Infrastructure reference:**
  - `manitec.pw` – primary domain.
  - `https://mail.manitec.pw` – custom mail client UI.
  - Render – FastAPI hosting.
  - DashNex – app and landing page platform (22+ apps).
  - Zoho Mail360 – mail API provider.
  - Cloudflare – DNS/CDN and SSL termination.

This file should live alongside other system/docs files and be updated whenever:
- A new DashNex app is added for a domain.
- The design system changes.
- The backend wiring (Render, Mail360, DNS) is significantly updated.
