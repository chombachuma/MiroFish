# Base44 dev notes

- Run: `docker compose -f docker-compose.base44.yml up -d`. Frontend = Vite (Vue) on 3000, backend = Flask on 5001 (debug reload).
- Vite proxies `/api` to `VITE_PROXY_TARGET` (set to `http://backend:5001` in compose; falls back to localhost for local dev).
- Backend refuses to start without `LLM_API_KEY` and `ZEP_API_KEY` (Config.validate). Dev placeholders let it boot, but graph building and simulation need real keys.
- First backend boot runs `uv sync` (heavy deps: camel-ai, oasis), which takes a few minutes. The venv is kept in a named volume.
- Backend `/` returns 404 on purpose. A quick check is `curl localhost:3000/api/graph/project/list` → 200.
