# HardShell Core

## Specification v1.2 (Final Integrated Version)

------------------------------------------------------------------------

# 1. Product Overview

## 1.1 Mission

Provide a secure, low-cost, and sustainable web foundation for small
organizations and individuals.

------------------------------------------------------------------------

## 1.2 Vision

Make "unbreakable web" the default.

-   Minimize security risk
-   Resist small traffic spikes
-   Reduce operational burden
-   Start small and grow

------------------------------------------------------------------------

# 2. Target Scale

-   Registered users: up to 10,000
-   MAU: up to 10,000
-   Low to medium update frequency
-   Read-heavy workload
-   Enterprise use cases are out of scope

------------------------------------------------------------------------

# 3. Domain Architecture

## 3.1 Core Domains

  Purpose       Domain
  ------------- -----------------
  Public site   www.example.com
  API           api.example.com
  Image / OGP   img.example.com

------------------------------------------------------------------------

## 3.2 Admin Domains (Prefix-based)

Controlled by environment variable: ADMIN_PREFIX

Example: ADMIN_PREFIX="cms"

  Purpose        Domain
  -------------- --------------------------
  Admin UI       cms_admin.example.com
  Registration   cms_register.example.com
  Login          auth-cms.example.com

If not set: - \_admin.example.com - \_register.example.com -
auth.example.com

------------------------------------------------------------------------

# 4. Core Principles

-   All writes are API-only
-   Unauthenticated access to admin/private/register returns 404
-   Public reads are cache-first
-   Fixed CORS allowlist

------------------------------------------------------------------------

# 5. Authentication

-   Firebase Auth (Email + Google OAuth)
-   Bearer ID token to API

Login flow sets cookie: seen_login=1 (180 days)

Cookie is UX-only, not used for authorization.

------------------------------------------------------------------------

# 6. Roles

1.  SuperAdmin
2.  Admin
3.  Designer
4.  Editor
5.  Reader
6.  Guest

------------------------------------------------------------------------

## 6.1 Role Rules

-   Only SuperAdmin can promote to Admin
-   Admin can promote to Designer or Editor
-   No self-promotion
-   Last SuperAdmin cannot be downgraded

------------------------------------------------------------------------

## 6.2 Soft Ban

-   members.isActive = false
-   Private access denied
-   Posting disabled
-   No physical deletion

Admin cannot ban another Admin. SuperAdmin can ban Admin or below.

------------------------------------------------------------------------

# 7. Content Model

Types: - page - post - gallery

Fields: - title - slug - bodyMd - visibility - status - publishedAt -
tagIds - summary - thumbnailAssetId - timestamps

------------------------------------------------------------------------

# 8. Image Pipeline

Original: original/{assetId}/ (immutable)

Derived: S (500px) M (1000px) L (2000px) webp only

URL: https://img.example.com/i/v1/{assetId}/{S\|M\|L}

Cache: public, max-age=31536000, immutable

Derived images are never auto-deleted.

------------------------------------------------------------------------

# 9. Tags

-   Dictionary-based (Admin only)
-   AND search up to 5 tags
-   Reverse index used
-   Merge supported

------------------------------------------------------------------------

# 10. Comments

-   Guest: reCAPTCHA + approval
-   Reader: immediate publish
-   API-only write

------------------------------------------------------------------------

# 11. SEO

-   sitemap.xml
-   feed.xml
-   Private pages: noindex
-   Generic OGP for private

------------------------------------------------------------------------

# 12. Caching

-   Public GET: max-age=60
-   Images: 1 year
-   Admin/private: no cache

------------------------------------------------------------------------

# 13. Audit Logs (BigQuery)

Dataset: audit Table: audit.events

Captured: - Content changes - Tag changes - Role changes - Soft bans -
AI publish overrides

Fields: eventId eventTime actorUid actorRole entityType entityId action
result beforeJson afterJson diffJson

------------------------------------------------------------------------

# 14. Non-Goals

-   Enterprise SSO
-   Unlimited tag filters
-   DRM-like image protection
-   Million-MAU scale design
-   Heavy workflow systems

------------------------------------------------------------------------

HardShell Core supports: - Small company websites - Personal blogs -
Lightweight communities - Photo-centric sites
