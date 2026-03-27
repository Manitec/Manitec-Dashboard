# DashNex Page Build Checklist

Use this checklist every time you create or edit a DashNex page for Manitec or Joe’s Faves. The goal is: fast builds, consistent look, nothing leaking, nothing weird.

---

## 1. Page purpose and URL

- [ ] Define the **single main goal** of the page  
      (e.g., capture email, send to app, explain a project).
- [ ] Choose the **correct domain**:
  - Brand-facing: `manitec.pw`
  - Personal / experimental: `joesfaves.com`
- [ ] Pick a **clean slug** (no junky auto-slugs):
  - Examples: `/banjoshire`, `/hexbot`, `/projects`, `/mail`.
- [ ] Verify DNS / mapping:
  - Domain/subdomain is routed through **Cloudflare**.
  - DashNex app is correctly connected to the right domain.  

---

## 2. Design system & layout

- [ ] Background set to **`#07070f`** (dark cyberpunk).
- [ ] Primary accent color: **`#9b30ff`** (purple).
- [ ] Secondary accent color: **`#00f5ff`** (cyan).
- [ ] Fonts:
  - **Space Grotesk** for headings and body.
  - **JetBrains Mono** for code/technical bits.
- [ ] Use **Bootstrap 4.1.3** grid / components where possible.
- [ ] Heroes:
  - Use `<img>` for hero images (no CSS `background-image`).
  - Set proper alt text for accessibility.
- [ ] Buttons:
  - Wrap groups of buttons in:

    ```css
    .mn-btn-group {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
    }
    ```

  - Use consistent primary button style for the main CTA.

---

## 3. Core content sections

Minimum sections for most pages:

- [ ] **Hero section**
  - Clear headline explaining what this is.
  - One short supporting sentence.
  - One primary CTA (button) wired to the main action
    (launch app, join Discord, open mail client, etc.).

- [ ] **What it is / who it’s for**
  - 2–3 bullets or short paragraphs.
  - Keep it in plain language; no corporate sludge.

- [ ] **How it connects to the rest of Manitec**
  - Links to relevant pieces:
    - `https://manitec.pw` for brand home.
    - `https://joesfaves.com` for personal hub.
    - `https://mail.manitec.pw` for custom mail client (when relevant).
    - `https://chat.manitec.pw` for AI / Hexbot (when relevant).
    - `https://manitec.github.io/Manitec-Dashboard/` for docs (when relevant).

- [ ] **Trust / context**
  - One short line about Manitec Future LLC / Joe, so the page doesn’t feel anonymous.

---

## 4. Tech hygiene

- [ ] **No secrets or user data** in DashNex:
  - No API keys.
  - No real user emails or tokens.
  - No database content.
- [ ] If the page needs “real” functionality:
  - It **links** or **embeds** a backend app (e.g., Render-hosted FastAPI),
    instead of doing it directly in DashNex.
- [ ] All external scripts/styles:
  - Are from trusted CDNs.
  - Are really necessary (no extra bloat if you can avoid it).

---

## 5. Copy & tone

- [ ] Voice is:
  - Playful, a bit chaotic, but still clear.
  - More cyberpunk hacker than corporate brochure.
- [ ] Headings:
  - Short and scannable.
  - Avoid walls of text.
- [ ] CTAs:
  - Start with verbs: “Enter Banjoshire”, “Launch Hexbot”, “Open Mail”.
- [ ] Make sure you answer:
  - What is this?
  - Why would someone care?
  - What do they do next?

---

## 6. QA before you publish

- [ ] Test on **mobile** and **desktop**.
- [ ] Check all links:
  - No broken links.
  - External links open in a new tab if appropriate.
- [ ] Verify main CTA goes exactly where it should:
  - Correct app URL or section.
- [ ] Check load feel:
  - No obviously broken assets (missing hero images, huge layout jumps).

---

## 7. After publishing

- [ ] Add the new page to:
  - The relevant **Projects / Apps** index (e.g., `joesfaves.com` projects page).
  - Any navigation menus where it makes sense.
- [ ] If it ties into infra:
  - Confirm DNS is correct in your infra list
    (`manitec.pw` primary domain, `mail.manitec.pw` webmail, Render, DashNex, Mail360, Cloudflare).  
- [ ] Make a quick note in your docs / dashboard repo so Future You remembers why this page exists.

---

Use this file as a living checklist – if you catch yourself fixing the same kind of mistake twice, add a bullet here so the next page build is brainless and consistent.
