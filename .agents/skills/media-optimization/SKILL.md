---
name: media-optimization
version: 2.0.0
origin: Adapted from supabase-media-pipeline & verify-portfolio-media in PORTFOLIO-DANILO-FINAL
description: Governs AVIF/WebP image optimization, responsive sizes, CLS-free aspect ratios, and viewport-gated HTML5 video lifecycles.
---

# Media Optimization Skill (`media-optimization`)

## 1. Purpose
Ensure high-resolution creative visuals (images, motion reels, case galleries) load instantaneously with zero layout shift (`CLS = 0`) and zero bandwidth waste.

## 2. When to Use
- When implementing `<SmartImage />`, `<AdaptiveVideo />`, case gallery blocks, or auditing `.context/ASSET-MANIFEST.md`.

## 3. When Not to Use
- Never mutate or delete production objects in Supabase Storage (`site-assets`, `portfolio-media`) or Cloudflare R2.

## 4. Input Contract
- `media_asset`: `MediaAsset` object (`kind`, `src`, `poster`, `alt`, `width`, `height`, `aspectRatio`).

## 5. Operational Instructions (Progressive Disclosure)
1. **Image Rules (`<SmartImage />`):**
   - Enforce `AVIF`/`WebP` delivery and accurate `sizes` attribute per grid span (`100vw`, `60vw`, `50vw`).
   - Apply `priority={true}` **only** to the single primary LCP hero asset per route.
   - Always specify `width`/`height` or `aspectRatio` container to guarantee `CLS = 0`.
2. **Video Rules (`<AdaptiveVideo />`):**
   - Default to `preload="none"` + mandatory optimized WebP `poster`.
   - Attach source and `.play()` (muted, playsInline) via `IntersectionObserver` only when entering the viewport; `.pause()` immediately on exit.
3. **Deep Reference:** Load `.context/MEDIA-ARCHITECTURE.md`.

## 6. Output Contract
- Optimized media renderer components and verified asset manifest entries.

## 7. Validation Criteria
- Passes `QG-10` (Image optimization) and `QG-11` (Video lifecycle & 100% HTTP `200 OK` asset reachability).

