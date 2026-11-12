# CODING RULES — GHOST PORTFOLIO 2.0

1. **TypeScript Strictness:** `strict: true` and `noUncheckedIndexedAccess: true` are mandatory. Zero implicit `any`, zero `@ts-ignore`.
2. **Next.js 16 Async Contracts:** Always `await params` and `await searchParams` in App Router pages and `generateMetadata`.
3. **Clean Imports & Modularity:** Use `@/*` path aliases (`src/*`). Keep components focused (`< 250` lines per file); extract sub-blocks when complexity grows.
4. **Zero Console Noise:** No `console.log` statements in committed `src/` files; use structured server logging or error boundaries.
5. **Comment Preservation:** Preserve meaningful architectural docstrings and never commit commented-out dead code.

