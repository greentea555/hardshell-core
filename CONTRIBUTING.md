# Contributing to HardShell Core

Thanks for considering contributing!

This project is developed **AI-first**. That means we value:
- clear specs
- deterministic behavior
- small changes
- strict boundaries (non-goals are important)

---

## Source of truth

- `SPEC.md` is the source of truth.
- If you want to change behavior, update `SPEC.md` first or in the same PR.

---

## AI-first workflow rules

When using AI to generate code:
1. **Start from contract**  
   - Update/confirm OpenAPI (`openapi/openapi.yaml`) before implementation.
2. **Small patches**  
   - One PR = one purpose.
3. **No silent feature creep**  
   - If the change adds scope, explicitly state why and update `SPEC.md`.
4. **Security stays structural**  
   - Keep the API-only write rule.
   - Keep the 404 masking rule for unauthenticated admin/private/register.
5. **Don’t “fix” style by changing behavior**  
   - Refactors should be behavior-preserving unless spec says otherwise.

---

## Pull request checklist

- [ ] Spec impact assessed (`SPEC.md` updated if needed)
- [ ] OpenAPI updated if API changed
- [ ] Added/updated tests (or explained why not needed)
- [ ] Security implications considered
- [ ] Audit events included for write operations

---

## Code style

- TypeScript strict mode
- Prefer explicit types at module boundaries
- Keep functions small and deterministic
- Avoid hidden global state

---

## Reporting security issues

Please do not open public issues for security problems.  
See `SECURITY.md`.