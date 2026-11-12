# SECURITY RULES — GHOST PORTFOLIO 2.0

1. **Secret Isolation:** Never commit `.env` files or secrets. Only `NEXT_PUBLIC_SITE_URL`, `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, and `NEXT_PUBLIC_ASSETS_CDN_URL` may use the `NEXT_PUBLIC_` prefix.
2. **Server-Only Enforcement:** Every file accessing `SUPABASE_SERVICE_ROLE_KEY` or server secrets must begin with `import 'server-only';`.
3. **Read-Only Public Posture:** Anonymous public visitors have `SELECT`-only access to published rows via Supabase RLS.
4. **Embed Sandboxing:** Never render untrusted or raw project HTML via `dangerouslySetInnerHTML` on the main origin; always isolate interactive embeds inside `<iframe sandbox="allow-scripts" referrerpolicy="no-referrer">`.
5. **CSP & Headers:** Maintain strict `Content-Security-Policy`, `HSTS`, `X-Frame-Options: DENY`, and `X-Content-Type-Options: nosniff` in `next.config.ts`.

