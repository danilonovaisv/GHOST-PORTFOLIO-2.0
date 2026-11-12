---
name: art-direction
version: 2.0.0
origin: Adapted from taste-skill (design-taste-frontend) & apple-design in Agent-Skills-Knowledge-Hub
description: Guides editorial composition, asymmetric Swiss grids, negative space pacing, typography pairing, and anti-slop visual craft.
---

# Art Direction Skill (`art-direction`)

## 1. Purpose
Enforce museum-grade editorial art direction, cinematic framing, and "invisible sophistication" across all layouts while preventing generic AI/SaaS design patterns.

## 2. When to Use
- When designing page layouts, composing Case Study blocks, selecting media aspect ratios, or reviewing visual prototypes.

## 3. When Not to Use
- Do not override usability, WCAG contrast, or Core Web Vitals budgets for decorative effects.

## 4. Input Contract
- `section_or_case`: Target page section or case study block sequence.
- `media_assets`: Available verified images/videos from `.context/ASSET-MANIFEST.md`.

## 5. Operational Instructions (Progressive Disclosure)
1. **Enforce Negative Space Mandate:** Preserve at least 35% Void Black (`#040013`) / Abyss negative space per viewport.
2. **Asymmetric Editorial Rhythm:** Alternate between full-bleed (`12-col`) cinematic frames, asymmetric splits (`7/5` or `8/4` columns), and focused editorial reading columns (`max-w-3xl`).
3. **Protect Foreground Hierarchy:** Keep WebGL shaders and atmospheric glows strictly behind editorial text (`--z-layer-base: 0` / `--z-layer-3d: 15` vs `--z-layer-content: 20`).
4. **Anti-Slop Guardrail:** Reject 3-column generic icon boxes, stock gradients, or bouncy hover scaling.
5. **Deep Reference:** Load `.context/CREATIVE-DIRECTION.md` for territory-specific mood rules.

## 6. Output Contract
- **Grid Column Allocation (`4 / 8 / 12` cols)**
- **Typographic Hierarchy & Token Mapping**
- **Media Framing & Aspect Ratio Spec**
- **Atmosphere & Z-Layer Assignment**

## 7. Validation Criteria
- Complies 100% with `.context/CREATIVE-DIRECTION.md` and `.context/DESIGN-SYSTEM.md`.

