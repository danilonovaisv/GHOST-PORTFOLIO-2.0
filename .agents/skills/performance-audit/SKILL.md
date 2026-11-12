---
name: performance-audit
version: 2.0.0
origin: Consolidated from web-perf & debug-optimize-lcp in Agent-Skills-Knowledge-Hub
description: Audits Core Web Vitals (LCP, INP, CLS), Next.js bundle sizes, media waterfalls, and WebGL frame rates against strict performance budgets.
---

# Performance Audit Skill (`performance-audit`)

## 1. Purpose
Ensure `GHOST-PORTFOLIO-2.0` achieves **Lighthouse Performance ≥ 90**, `LCP < 2.5s`, `INP < 200ms`, `CLS < 0.1`, and sustained `60 FPS` interactions.

## 2. When to Use
- During Phase 10 (`10-performance-audit.md`) and before any release sign-off.

## 3. When Not to Use
- Never report synthetic estimates as actual measurements; always run Lighthouse / DevTools trace or bundle analysis.

## 4. Input Contract
- `build_output`: Production build (`pnpm build`) and running preview server.

## 5. Operational Instructions (Progressive Disclosure)
1. **Bundle Budget Check:** Verify route First Load JS `< 180KB` for editorial pages; confirm `three` and `@react-three/fiber` are dynamically imported only in isolated client islands.
2. **LCP Waterfall Check:** Confirm the hero LCP asset is preloaded (`fetchPriority="high"`), served in `AVIF`/`WebP`, and not blocked by client hydration or WebGL initialization.
3. **CLS & Layout Stability:** Confirm `CLS < 0.1` by verifying explicit aspect-ratio reservations on all media blocks and `font-display: swap` metric matching.
4. **INP & Main-Thread Budget:** Profile scroll and filter interactions to confirm zero long tasks (`> 50ms`) blocking pointer response.

## 6. Output Contract
- Performance Audit Report (`docs/audits/PERFORMANCE-AUDIT.md`) covering `QG-09`, `QG-10`, `QG-11`, and `QG-12`.

## 7. Validation Criteria
- Mobile & Desktop Lighthouse Performance `≥ 90` (`QG-09` = `PASS`).

