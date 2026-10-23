# Supply Proof

Document delivery discrepancies, keep evidence with each case, and prepare supplier follow-ups. This checkout is still a local prototype: the UI persists cases in `localStorage`, and the API currently exposes a health check only.

## Run & Operate

- `pnpm --filter @workspace/supply-proof run dev` — frontend (default port 5173)
- `pnpm --filter @workspace/api-server run dev` — API server (default port 8080)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only; needs `DATABASE_URL`)

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- UI: Vite 7, React 19, Tailwind 4, wouter
- API: Express 5
- DB: PostgreSQL + Drizzle ORM (schema not implemented yet)
- Validation: Zod, `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- API build: esbuild ESM bundle

## Where things live

- Product UI: `artifacts/supply-proof/src/App.tsx`
- Theme: `artifacts/supply-proof/src/index.css`
- API entry: `artifacts/api-server/src/index.ts`
- OpenAPI contract: `lib/api-spec/openapi.yaml`
- Drizzle schema: `lib/db/src/schema/index.ts`

## Architecture decisions

- Prototype first: the UI does not call the generated React Query client yet.
- Evidence uploads store filenames only; files are not persisted.
- Auth screens are cosmetic so the workspace can be opened without accounts.
- Native binary pnpm overrides were removed so Windows and macOS can install Vite/esbuild.

## Product

- Capture ordered vs received quantities and issue type
- Attach receipt/photo metadata to a case
- Copy a supplier follow-up message
- Track status and recorded recoveries

## Gotchas

- Use pnpm, not npm or yarn (`scripts/ensure-pnpm.mjs` enforces this).
- `lib/db` throws if imported without `DATABASE_URL`.
- Replit still injects `PORT` / `BASE_PATH`; local defaults exist in Vite and the API.
