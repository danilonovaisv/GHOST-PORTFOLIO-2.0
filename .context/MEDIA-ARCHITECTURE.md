# MEDIA ARCHITECTURE — GHOST PORTFOLIO 2.0

**Phase:** 02 — Media Pipeline & Performance Engineering  
**Active Personas:** Media Pipeline Engineer (`AG-11`), Performance Auditor (`AG-14`), Creative Technology Engineer (`AG-09`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Zero-Placeholder & Verified Asset Mandate

Every image, video, brand logo, and 3D texture in `GHOST-PORTFOLIO-2.0` must resolve from a verified entry in `.context/ASSET-MANIFEST.md` (sourced from Supabase Storage buckets `site-assets`, `portfolio-media`, or Cloudflare R2 `assets.portfoliodanilo.com`).

---

## 2. Image Delivery Pipeline (`<SmartImage />`)

1. **Format & Compression:**
   - Primary delivery in `AVIF` and `WebP` via `next/image` custom loader or pre-optimized CDN variants.
   - Automatic `sizes` attribute enforcement based on grid span:
     - Full-bleed (`12 cols`): `100vw`
     - Flagship split (`7 cols`): `(max-width: 768px) 100vw, (max-width: 1200px) 60vw, 980px`
     - Grid card (`6 cols` / `4 cols`): `(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 540px`
2. **LCP Prioritization:**
   - Only the primary above-the-fold Hero media asset receives `priority={true}` (`fetchPriority="high"`).
   - All below-the-fold case gallery images use native `loading="lazy"` and `decoding="async"` with a low-contrast `#0B0D3A` shimmer placeholder to guarantee `CLS = 0`.

---

## 3. Adaptive Video Pipeline (`<AdaptiveVideo />`)

Video-heavy portfolios frequently fail Core Web Vitals due to simultaneous video preloading. `GHOST-PORTFOLIO-2.0` enforces a strict **Viewport-Gated Video Lifecycle**:

1. **Zero Eager Video Download on Initial Load:**
   - Video cards and case study video blocks initialize with `preload="none"` and a lightweight optimized WebP `poster` frame.
2. **IntersectionObserver Lifecycle:**
   - **Approaching Viewport (`rootMargin: "200px"`):** Switches to `preload="metadata"` or attaches `<source>`.
   - **Inside Viewport (`threshold: 0.25`):** Calls `.play()` (muted, inline, loop for ambient previews) only if `prefers-reduced-motion: no-preference`.
   - **Leaving Viewport (`threshold: 0`):** Immediately calls `.pause()` to free GPU/decoder threads.
3. **Hover Preview Throttling (Desktop Portfolio Cards):**
   - Hovering a project card triggers video playback after a `120ms` intent debounce, cancelling immediately on pointer leave.

---

## 4. WebGL & Three.js Performance Budget (`<WebGLBoundary />`)

1. **Isolated Client Bundles:**
   - Three.js and `@react-three/fiber` are never imported in global layouts or Server Components; they load asynchronously via `next/dynamic(..., { ssr: false })`.
2. **Strict GPU & Frame Budgets:**
   - Device Pixel Ratio capped at `dpr={[1, 1.5]}` on mobile and `dpr={[1, 2]}` on desktop.
   - `frameloop="demand"` or automatic pause when the canvas leaves the viewport.
   - Automatic fallback to static CSS atmospheric gradient (`--color-abyss-start` → `--color-background`) when:
     - `prefers-reduced-motion: reduce` is active, OR
     - Battery Saver / low-power CPU is detected, OR
     - WebGL context creation fails.

