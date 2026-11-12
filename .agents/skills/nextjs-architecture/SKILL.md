---
name: nextjs-architecture
version: 2.0.0
origin: Adapted from ghost-architect & nextjs-app-router-caching in PORTFOLIO-DANILO-FINAL and Agent-Skills-Knowledge-Hub
description: Governs Next.js 16 App Router architecture, Server/Client Component boundaries, generateStaticParams, unstable_cache, and error boundaries.
---

# Next.js 16 Architecture Skill (`nextjs-architecture`)

## 1. Purpose
Enforce clean, resilient, high-performance Next.js 16 App Router patterns across `src/app/` and `src/lib/`.

## 2. When to Use
- When scaffolding routes, data fetchers, caching layers, Server Actions, middleware, or `error.tsx` boundaries.

## 3. When Not to Use
- Do not add `'use client'` to route `page.tsx` or `layout.tsx` files; keep pages as async Server Components.

## 4. Input Contract
- `route_or_module`: Target route segment in `src/app/` or data module in `src/lib/`.

## 5. Operational Instructions (Progressive Disclosure)
1. **Verify via Context7 First:** Query `/vercel/next.js/v16.4.5` when using framework APIs (`unstable_cache`, `revalidateTag`, `generateStaticParams`, `generateMetadata`).
2. **Server-First Default:** Fetch and validate all content in Server Components via `src/lib/data/` repositories with local snapshot fallback.
3. **Mandatory Error Boundaries:** Every route group/segment must include a Client Component `error.tsx` boundary with a `retry()` handler.
4. **Async Params Contract:** In Next.js 15/16, `params` and `searchParams` are Promises (`params: Promise<{ slug: string }>`)—always `await params`.
5. **Deep Reference:** Load `.context/TECHNICAL-ARCHITECTURE.md` for system diagrams and caching rules.

## 6. Output Contract
- Strictly typed Next.js 16 route modules, data repositories, and error boundaries.

## 7. Validation Criteria
- `QG-01` (`pnpm typecheck`), `QG-02` (`pnpm lint`), and `QG-15` (`pnpm build`) pass with zero errors.

