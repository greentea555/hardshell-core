# HardShell Core

**HardShell Core** is a lightweight, secure web foundation for small sites and lightweight communities.

It prioritizes:
- **Structural security** (secure by design, not by endless configuration)
- **Operational simplicity** (works with low update frequency and small teams)
- **Resilience** (doesn’t fall over from a small “buzz”)
- **Low cost** (serverless-first, cache-first)

> This project is intentionally opinionated. If you need enterprise-grade features, this is not the right tool.

---

## What it provides

- **Content API** (cache-first, public/private)
- **Image pipeline** (immutable originals + derived S/M/L, CDN-friendly)
- **Tags & Gallery** (dictionary-based tags, multi-tag AND up to 5, tag merge)
- **Lightweight community** (comments, surveys, soft-ban)
- **Audit logging** (BigQuery events with diffs)
- **Role model** (SuperAdmin / Admin / Designer / Editor / Reader / Guest)

---

## Who it’s for

HardShell Core is designed for:
- small company websites (news / pages / contact)
- personal blogs (SEO-friendly publishing)
- lightweight member areas (private pages)
- photo-heavy sites (tag-based galleries)

---

## Non-goals

HardShell Core does **not** aim to provide:
- enterprise SSO/SAML
- complex workflow approvals
- unlimited tag filtering (AND is capped at 5)
- DRM-like protection / member-only image delivery
- “million MAU” architecture by default
- a no-code page builder

See `SPEC.md` for details.

---

## Architecture (high level)

**Recommended production split**
- `apps/web` → Public site (Nuxt SSR)
- `apps/api-cloudrun` → Core API (Cloud Run, TS)
- `apps/img` → Image & OGP service (Cloud Run + CDN)
- `apps/api-nitro` → Optional Nitro adapter for local dev / lightweight deployments

**All writes are API-only** (no direct Firestore/Storage writes from clients).

---

## Repository layout (monorepo)

```
hardshell-core/
  SPEC.md
  README.md
  AGENTS.md
  openapi/
    openapi.yaml
  packages/
    core/              # business rules: usecases/policy/audit/diff
    clients/           # firestore/storage/bigquery/recaptcha (thin)
    shared/            # shared types/errors/utils
  apps/
    web/               # Nuxt 4 + Pug (SSR) for www.*
    api-nitro/         # Nitro API adapter (optional)
    api-cloudrun/      # Cloud Run API (prod)
    img/               # Image + OGP service (prod) with CDN
```

**Rule:** business rules belong in `packages/core`. Apps are thin adapters.

---

## Getting started (local)

> Placeholder. This will be filled as the code lands.

Typical workflow (planned):
1. Install dependencies
2. Run dev servers (web + api-nitro)
3. Run lint/test

---

## Configuration (planned)

- `ADMIN_PREFIX`
- CORS allowlist
- Firebase / GCP credentials
- BigQuery dataset/table for audit logs

Details will be documented under `docs/` or in `SPEC.md`.

---

## Contributing

This project is developed **AI-first**.

- `SPEC.md` is the source of truth
- Prefer OpenAPI → implementation → tests
- Keep PRs small and scoped

See `CONTRIBUTING.md`.

---

## License

Apache-2.0. See `LICENSE` and `NOTICE`.
