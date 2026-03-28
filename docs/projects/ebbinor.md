# Ebbinor

**What it is:** A custom voxel game built on the Luanti engine (formerly Minetest). Started as a fun project with Joe's kids — they encouraged him to keep building it into what it is today.

**Tagline:** Roleplay, sandbox, survival, or creative fun.

![Ebbinor](https://i.postimg.cc/2j4Hfmmj/Screenshot-2026-03-28-055948.png)

**Download:** [ebbinor.joesfaves.com](https://ebbinor.joesfaves.com)

## Stack

- **Engine:** Luanti (formerly Minetest) — with custom core engine modifications
- **Content:** Collection of custom mods and textures — no built-in worlds included
- **Distribution:** Windows installer + Android APK

## Current Playability

- ✅ Download and play locally (Windows / Android)
- ✅ Can join most available Luanti servers
- ✅ Can run a local-only server
- ❌ No persistent dedicated online server yet

## Status

**Maintenance mode** — not actively developed right now. Core is stable.

## Dedicated Server Goal

The primary goal is a persistent always-on dedicated server for Ebbinor so players don't need a local server to play together.

**Current plan:** Oracle Cloud Free Tier (Ampere A1 — 4 OCPU / 24GB RAM)
- A1 instance not yet obtained (out of capacity)
- VM.Standard.E2.1.Micro (1GB RAM) available as fallback for small player counts
- Port: UDP 30000
- Server will need Ebbinor's custom mods/content deployed alongside Luanti

## Tools Used

| Tool | Purpose |
|---|---|
| Luanti Engine | Core game engine |
| Cloudflare | DNS & CDN |
| Namecheap | Domain management |
| NightCafe | AI art / texture generation |

## Links

- Site: [ebbinor.joesfaves.com](https://ebbinor.joesfaves.com)
- GitHub: [Manitec/Ebbinor](https://github.com/Manitec/Ebbinor)
- Engine: [luanti.org](https://www.luanti.org)
