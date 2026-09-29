# AGENTS.md

## Project Overview

Minimal static HTML site — a single `index.html` with no backend, no build step, no dependencies. References `mtfoda.css` which does not exist (results in a harmless 404).

## Running in Base44

Served by `nginx:alpine` via `docker-compose.base44.yml`. The repo root is bind-mounted (read-only) at `/usr/share/nginx/html` and exposed on host port 3000.

- **Start:** `docker compose -f docker-compose.base44.yml up -d`
- **Health:** `curl http://localhost:3000/` returns the HTML page.
- **Edits:** Changes to `index.html` (or any file in the repo root) are live — just refresh the browser. No build or restart needed.

## Quirks

- The repo root directory had mode `700`; nginx's worker process (non-root) couldn't read it, causing 403. Fixed by `chmod 755 .` on the host. If a fresh clone shows 403, re-run that chmod.
