# HardShell Core

**HardShell Core** is a lightweight, secure web foundation for small sites and small communities.

It prioritizes:
- **Structural security** (secure by design, not by endless configuration)
- **Operational simplicity** (works with low update frequency and small teams)
- **Resilience** (doesn’t fall over from a small “buzz”)
- **Low cost** (serverless-first, cache-first)

> This project is intentionally opinionated. If you need enterprise-grade features, this is not the right tool.

---

## What it is

HardShell Core is a **GCP/Firebase-first** foundation that provides:
- Headless content API (cache-first)
- Image pipeline (original immutable + derived S/M/L)
- Tag dictionary + gallery (multi-tag AND up to 5)
- Lightweight community features (comments / surveys)
- Membership (Reader) + staff roles (Editor/Designer/Admin/SuperAdmin)
- Audit logs exported to BigQuery (including diffs)

---

## What it is NOT

HardShell Core does **not** aim to be:
- A full enterprise CMS (SSO/SAML, advanced workflows)
- A no-code page builder
- A high-traffic (million MAU) platform
- A DRM-like “content protection” system

See `SPEC.md` for the full scope and non-goals.

---

## Tech stack

- TypeScript (Node.js)
- Google Cloud Run
- Firebase Auth
- Firestore + Cloud Storage
- BigQuery (audit logs)
- Cloud CDN (recommended) for `img.*`

---

## Core principles

- **Write is API-only**: clients never write to Firestore/Storage directly.
- **Cache first**: public reads are cached (60s + ETag).
- **Quiet private**: unauthenticated access is masked as 404; private OGP is generic.
- **Deterministic images**: S/M/L only, webp, derived kept (no access-based deletion).
- **Governed tags**: dictionary-only, Admin-managed, merge supported; AND max 5.
- **Auditability**: BigQuery stores who changed what and when (with diffs).

---

## Repository layout (initial)

- `SPEC.md` — product spec (source of truth)
- `openapi/` — API contract (OpenAPI)
- `src/` — implementation
- `docs/` — documentation (optional)
- `.github/` — templates & automation

---

## Contributing

HardShell Core is developed with **AI-first workflows**.
Please read `CONTRIBUTING.md` before opening PRs.

---

## License

TBD (choose one: Apache-2.0 / MIT)