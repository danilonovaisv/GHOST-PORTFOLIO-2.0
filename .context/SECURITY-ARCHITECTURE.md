# SECURITY ARCHITECTURE — GHOST PORTFOLIO 2.0

**Phase:** 02 — Security & Infrastructure Governance  
**Active Personas:** Security Auditor (`AG-15`), Backend Engineer (`AG-10`), Frontend Architect (`AG-06`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Core Security Principles

1. **Zero Secret Exposure in Client Bundle:**
   - Only `NEXT_PUBLIC_SITE_URL`, `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, and `NEXT_PUBLIC_ASSETS_CDN_URL` may be prefixed with `NEXT_PUBLIC_`.
   - Service role keys (`SUPABASE_SERVICE_ROLE_KEY`), revalidation tokens (`REVALIDATION_SECRET`), and R2 credentials are strictly isolated to server-only modules enforced via `import 'server-only'`.
2. **Public Portfolio Read-Only Posture:**
   - The public web application performs **zero database mutations** from anonymous sessions, except rate-limited contact inquiries (handled via validated Server Action with Turnstile/honeypot protection) and rate-limited client error telemetry (`/api/telemetry/error`).
3. **Least-Privilege MCP & Agent Governance:**
   - Agents operate under strict tool scoping: UI/Motion/Design agents have zero access to database mutation or deployment tools; production deployment requires explicit human confirmation.

---

## 2. Environment Variable Contract (`.env.example`)

Validated at build and startup via `src/lib/validation/env.ts` using Zod:

```ini
# Public Runtime Variables (Safe for Client & Server)
NEXT_PUBLIC_SITE_URL="https://portfoliodanilo.com"
NEXT_PUBLIC_SUPABASE_URL="https://umkmwbkwvulxtdodzmzf.supabase.co"
NEXT_PUBLIC_SUPABASE_ANON_KEY=""
NEXT_PUBLIC_ASSETS_CDN_URL="https://assets.portfoliodanilo.com"

# Server-Only Variables (NEVER exposed to browser; enforced via 'server-only')
SUPABASE_SERVICE_ROLE_KEY=""
REVALIDATION_SECRET=""
CONTACT_WEBHOOK_URL=""
```

---

## 3. HTTP Security Headers & Content Security Policy (CSP)

Configured in `next.config.ts`:

| Header | Policy Value | Purpose |
| :--- | :--- | :--- |
| `Content-Security-Policy` | Strict allowlist for `'self'`, `*.supabase.co`, `assets.portfoliodanilo.com`, `*.r2.dev`, `www.youtube-nocookie.com` | Mitigates XSS, unauthorized data exfiltration, and clickjacking |
| `Strict-Transport-Security` | `max-age=63072000; includeSubDomains; preload` | Enforces HTTPS everywhere |
| `X-Frame-Options` | `DENY` | Prevents clickjacking embeds of the portfolio |
| `X-Content-Type-Options` | `nosniff` | Prevents MIME-sniffing attacks |
| `Referrer-Policy` | `strict-origin-when-cross-origin` | Protects visitor privacy on external links |
| `Permissions-Policy` | `camera=(), microphone=(), geolocation=(), payment=()` | Disables unused sensitive browser APIs across public routes |

---

## 4. Safe HTML / Interactive Embed Sandboxing

For projects using `interactive-embed` or `thumbnailHtml` (carried over from `MasterProjectTemplateV3`):
- Raw HTML embeds are **never** injected via unsanitized `dangerouslySetInnerHTML` on the main document origin.
- Interactive HTML embeds must render inside a sandboxed `<iframe sandbox="allow-scripts" referrerpolicy="no-referrer">` or be mapped to pre-verified React/R3F components registered in `src/components/three/registry.ts`.

