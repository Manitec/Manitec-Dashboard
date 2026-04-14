# Manitec Command Hub

**What it is:** The machine-facing API backend for the Manitec empire — a private FastAPI service that gives bots, dashboards, and automation scripts a single credentialed endpoint for all deploy actions, project status, and infrastructure commands.

## Stack

- **Framework:** FastAPI (Python)
- **Hosting:** Vercel (serverless)
- **Auth:** API key — `HEXBOT_API_KEY` / `MANIBOT_API_KEY` env vars
- **Project registry:** `project-registry.json` — single source of truth for all empire projects

## Modules

| File | Role |
|---|---|
| `deployer.py` | Triggers Vercel redeploys via API |
| `inspector.py` | Reads project status, uptime, and health |
| `registry.py` | Reads/queries `project-registry.json` |
| `kb_search.py` | Searches the Manitec knowledge base |
| `mail360_client.py` | Zoho Mail360 API integration |
| `task_tracker.py` | GitHub Issues task sync |
| `auth.py` | API key validation middleware |

## Features (Live ✅)

- API key auth on all routes
- Deploy trigger endpoint — bots and dashboards call this instead of Vercel directly
- Project registry read — structured JSON source of truth for all projects
- Health check endpoint — `/health`

## Next Steps

- [ ] Control Hub routes all deploy actions through here (currently calls Vercel directly)
- [ ] HexBot wired to deploy and status endpoints
- [ ] Mail360 integration fully tested end-to-end
- [ ] Task tracker sync with GitHub Issues live

## Lessons Learned

- FastAPI on Vercel requires `vercel.json` with explicit route rewrites to `main.py`
- Keep bot API keys separate — one per consumer so you can revoke individually
- `project-registry.json` as a flat JSON file beats a database for this scale
