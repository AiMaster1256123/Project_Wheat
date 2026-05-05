# AI Gateway Stack

Self-hosted AI gateway stack with:

- Open WebUI
- LiteLLM proxy
- PostgreSQL
- Redis
- Prometheus
- Grafana
- Caddy auth proxy for monitoring

## Quick start

1. Copy `.env.example` to `.env` and set secrets.
2. Start: `docker compose up -d`
3. Open:
   - Open WebUI: `http://localhost:3000`
   - LiteLLM: `http://localhost:4000`

## Monitoring with auth proxy

- Grafana via Caddy: `http://localhost:8081`
- Prometheus via Caddy: `http://localhost:8082`

Default auth user is `monitoradmin` (change in `caddy/Caddyfile`).
