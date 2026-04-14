# Mailserver

**What it is:** A custom Zoho Mail360 client — a FastAPI backend + webmail
frontend that wraps the Zoho Mail360 API and serves internal Manitec email
through a custom interface.

**Repo:** [Manitec/mailserver](https://github.com/Manitec/mailserver)

## Stack

- **Backend:** FastAPI (Python)
- **Hosting:** Render
- **Email provider:** Zoho Mail360 API
- **DNS/CDN:** Cloudflare
- **Domain:** `mail.manitec.pw` (password protected, internal use)

## Status: ✅ Active

Created March 2026. Powers internal Manitec email through a custom
webmail interface rather than Zoho's native UI.

## Features

- Custom webmail frontend served at a Manitec subdomain
- FastAPI backend wrapping Zoho Mail360 API
- Password-protected — internal access only

## Next Steps

- [ ] Wire Mail360 client into Command Hub (`mail360_client.py` module exists, needs endpoint)
- [ ] Add send/reply support if not already implemented
- [ ] Document API key rotation process

## Tasks

--8<-- "meta/tasks/tasks-mailserver.md"
