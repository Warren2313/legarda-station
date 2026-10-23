# Supply Proof

Local prototype for documenting B2B delivery discrepancies: record short counts, keep evidence with the case, prepare a supplier follow-up, and track recovery. Cases and settings are stored in the browser (`localStorage`). There is no real sign-in, email send, or database persistence yet.

## Prerequisites

- Node.js 22+ (Node 24 is what Replit used)
- [pnpm](https://pnpm.io/installation)

## Run locally
Download the source code, and then:
```bash
$ cd C:/Users/[username]/Documents/GitHub/legarda-station
pnpm install
pnpm dev
```

The UI is at [http://localhost:5173](http://localhost:5173).

Optional API (health check only):

```bash
pnpm dev:api
```

Defaults to port `8080`. Vite proxies `/api` to that port, so `GET /api/healthz` works from the frontend origin.

## Other commands

| Command | Purpose |
| --- | --- |
| `pnpm run typecheck` | Typecheck libraries and artifacts |
| `pnpm run build` | Typecheck and build all packages |
| `pnpm --filter @workspace/api-spec run codegen` | Regenerate API client + Zod from OpenAPI |
| `pnpm --filter @workspace/db run push` | Push Drizzle schema (needs `DATABASE_URL`) |

## Layout

- `artifacts/supply-proof` — the product UI
- `artifacts/api-server` — Express API (`/api/healthz` today)
- `lib/api-spec` — OpenAPI source of truth
- `lib/db` — Drizzle schema (empty until persistence is added)
- `artifacts/mockup-sandbox` — Replit canvas preview (unused in this prototype)

Environment overrides: `PORT`, `BASE_PATH`, `API_PORT` for the UI; `PORT` for the API.
