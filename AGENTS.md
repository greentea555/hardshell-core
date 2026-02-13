# AGENTS.md (HardShell Core)

This repository is a monorepo. Follow SPEC.md as the source of truth.

## Boundaries
- Business rules MUST live in `packages/core`.
- Apps under `apps/*` are thin adapters (routing, HTTP, SSR rendering).
- Clients MUST NOT write directly to Firestore/Storage. Writes are API-only.

## Repo layout
- packages/core: usecases, policy (roles/ban), audit event builder, diff (JSON Patch)
- packages/clients: Firestore/Storage/BigQuery/reCAPTCHA clients (thin)
- apps/web: Nuxt (SSR) public/private site
- apps/api-nitro: Nitro adapter (local dev / optional)
- apps/api-cloudrun: Cloud Run API service
- apps/img: image & OGP service (Cloud Run + CDN)

## Development rules
1) Update OpenAPI first when changing HTTP behavior.
2) Make small changes. One PR = one purpose.
3) Do not add features outside SPEC.md.
4) Prefer deterministic behavior. Avoid hidden global state.

## Safety rules
- Never run destructive commands (rm -rf, format, etc.).
- Request review for all terminal commands.
- Do not access files outside the workspace.