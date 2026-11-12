---
name: security-review
version: 2.0.0
origin: Consolidated from security-audit & cc-skill-security-review in Agent-Skills-Knowledge-Hub
description: Audits secret isolation, server-only boundaries, Content-Security-Policy (CSP), Supabase RLS policies, and iframe sandboxing.
---

# Security Review Skill (`security-review`)

## 1. Purpose
Protect `GHOST-PORTFOLIO-2.0` and the shared Supabase/CDN infrastructure against credential leaks, XSS, clickjacking, unauthorized data mutations, and dependency vulnerabilities.

## 2. When to Use
- Before committing environment/config changes, when modifying `next.config.ts` or `src/lib/supabase/`, and during Pre-Release (`13-pre-release.md`).

## 3. When Not to Use
- Never echo or log secret values during a scan.

## 4. Input Contract
- `target_scope`: Repository source files, `next.config.ts`, `.env.example`, and Supabase schema policies.

## 5. Operational Instructions (Progressive Disclosure)
1. **Secret & Env Boundary Check:** Verify that only approved public variables use the `NEXT_PUBLIC_` prefix and all privileged modules import `'server-only'`.
2. **CSP & HTTP Headers Check:** Verify `Content-Security-Policy`, `Strict-Transport-Security`, `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, and `Referrer-Policy` in `next.config.ts`.
3. **Database RLS Check:** Confirm that public portfolio queries use read-only policies (`SELECT` where `is_published = true`) and never touch legacy production tables destructively.
4. **Embed Sandboxing:** Confirm any interactive HTML embed renders inside a restricted `<iframe sandbox="allow-scripts">`.

## 6. Output Contract
- Security Audit Report (`docs/audits/SECURITY-AUDIT.md`) with `QG-14` status (`PASS` / `FAIL` / `NOT VERIFIED`).

## 7. Validation Criteria
- `QG-14` reports `PASS` with zero exposed secrets and full header/RLS compliance.

