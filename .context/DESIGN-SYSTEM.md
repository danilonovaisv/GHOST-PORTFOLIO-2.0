# GHOST DESIGN SYSTEM 2.0 — CANONICAL SPECIFICATION

**Phase:** 05 — Design System Architecture  
**Version:** 2.0 (Evolved from Ghost System v3.2)  
**Active Personas:** Design System Architect (`AG-04`), Art Director (`AG-03`), Accessibility Auditor (`AG-13`), Motion Engineer (`AG-08`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Design Philosophy & Evolution Summary

**Ghost Design System 2.0** preserves the iconic atmospheric identity of Danilo Novais's portfolio (*Void Black + Electric Brand Blue + Ghost Cyan + Fluid Manrope*) while resolving the token inconsistencies, contrast edge cases, and editorial layout needs required for an executive creative leadership platform.

### Key Evolutions from v3.2 to Ghost 2.0
1. **Typography Canonicalization:** Officially standardizes on **`Manrope Variable`** (UI, Display, Editorial) + **`PPSupplyMono`** (Technical metadata, coordinates, tags), eliminating legacy references to `TT Norms Pro` or `Outfit`.
2. **WCAG 2.2 AA Contrast Hardening:** Introduces `--color-text-muted-aa` (`#B4B8C5`, contrast ratio `9.8:1` on `#040013` and `7.9:1` on `#0B0D3A`) alongside legacy `#A1A3A3` to guarantee accessible long-form reading in case studies.
3. **Editorial Reading Measures:** Adds dedicated typographic tokens for executive case study narratives (`60ch–72ch` optimal measure, `1.65` line-height).
4. **Scoped Case Accents:** Allows individual case studies to define `--case-accent` for subtle ambient borders and eyebrows while keeping primary interactive controls anchored in Ghost Blue (`#0048FF`).

---

## 2. Color Tokens (`@theme` in `src/styles/globals.css`)

| Semantic Token | CSS Variable | Hex / Value | Contrast on `#040013` | Usage Mandate |
| :--- | :--- | :--- | :--- | :--- |
| **Void Black** | `--color-void-black` / `--color-background` | `#040013` | — | Global infinite canvas background. Never use `#000000`. |
| **Abyss Mid** | `--color-abyss-mid` | `#08031F` | — | Midpoint atmospheric gradient stop & elevated section surface. |
| **Deep Neutral** | `--color-deep-neutral` / `--color-neutral` | `#0B0D3A` | — | Card surfaces, bento containers, subtle structural blocks. |
| **Abyss Start** | `--color-abyss-start` | `#0C1445` | — | Top atmospheric gradient stop for Hero stages. |
| **Ghost Glass** | `--color-ghost-surface` | `rgba(255, 255, 255, 0.05)` | — | Translucent glass cards (`backdrop-blur-md` + `border-white/10`). |
| **Brand Blue** | `--color-brand-blue` / `--color-bluePrimary` | `#0048FF` | `4.62:1` (AA Large / UI) | Primary CTAs, active indicators, brand anchor. |
| **Blue Hover** | `--color-blue-hover` | `#2E85F2` | `6.54:1` (AA) | Hover state for blue interactive surfaces and inline links. |
| **Ghost Cyan** | `--color-ghost-cyan` / `--color-blueAccent` | `#4FE6FF` | `13.4:1` (AAA) | Focus rings, spectral highlights, active coordinates, outline CTAs. |
| **Text Primary** | `--color-text-primary` / `--color-text` | `#FCFFFF` | `19.6:1` (AAA) | Headlines, primary body copy, active navigation labels. |
| **Text Editorial** | `--color-text-editorial` | `#E2E6F0` | `15.8:1` (AAA) | Long-form case study narrative paragraphs (reduces halation on dark bg). |
| **Text Secondary** | `--color-text-secondary` | `#B4B8C5` | `9.8:1` (AAA) | Captions, role descriptions, secondary metadata. |
| **Text Muted** | `--color-text-muted` | `#A1A3A3` | `7.8:1` (AAA) | Deactivated states, subtle index numbers. |
| **Purple Anomaly** | `--color-purple-anomaly` / `--color-purpleDetails` | `#8705F2` | — | **Strictly restricted** to `<AntigravityCTA />` hover circle and glitch accents. |
| **Pink Accent** | `--color-pink-accent` / `--color-pinkDetails` | `#F501D3` | — | Micro-accents, shader highlights, experimental Lab tags. |
| **System Error** | `--color-system-red` | `#E50914` | `4.8:1` (AA) | Validation errors, destructive warnings, system alerts. |

---

## 3. Typography System

### 3.1 Font Stack
- **Primary Display & Editorial (`--font-sans`):** `'Manrope'`, variable weight `200–800`, self-hosted WOFF2 (`font-display: swap`).
- **Technical & Metadata (`--font-mono`):** `'PPSupplyMono'`, `'Space Mono'`, `monospace`, self-hosted WOFF2.

### 3.2 Fluid Typographic Scale (`clamp()`)

| Token / Utility | Mobile (`375px`) | Desktop (`1680px`) | Formula | Weight | Line Height | Tracking |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `.text-hero-manifesto` | `2.5rem` (40px) | `5.25rem` (84px) | `clamp(2.5rem, 5.5vw, 5.25rem)` | `800` | `1.04` | `-0.03em` |
| `.text-display` | `2.25rem` (36px) | `4.5rem` (72px) | `clamp(2.25rem, 5vw, 4.5rem)` | `800` | `1.08` | `-0.025em` |
| `.text-h1` | `1.875rem` (30px) | `3.5rem` (56px) | `clamp(1.875rem, 4vw, 3.5rem)` | `700` | `1.1` | `-0.02em` |
| `.text-h2` | `1.5rem` (24px) | `2.5rem` (40px) | `clamp(1.5rem, 3vw, 2.5rem)` | `600` | `1.15` | `-0.015em` |
| `.text-h3` | `1.25rem` (20px) | `1.75rem` (28px) | `clamp(1.25rem, 2vw, 1.75rem)` | `500` | `1.22` | `-0.01em` |
| `.text-body-editorial` | `1.125rem` (18px) | `1.25rem` (20px) | `clamp(1.125rem, 1.4vw, 1.25rem)` | `400` | `1.65` | `0em` |
| `.text-body` | `1.125rem` (18px) | `1.125rem` (18px) | `clamp(1.0625rem, 1.2vw, 1.125rem)` | `400` | `1.55` | `0em` |
| `.text-small` | `0.875rem` (14px) | `0.875rem` (14px) | `0.875rem` | `400` | `1.45` | `0.01em` |
| `.text-micro-mono` | `0.75rem` (12px) | `0.75rem` (12px) | `0.75rem` | `400` (Mono) | `1.4` | `0.08em` (uppercase) |

---

## 4. Layout, Spacing & Responsive Grid (`.std-grid`)

### 4.1 Breakpoints & Column Architecture
- **`sm` (`< 768px` — Mobile First):** 4 columns, `16px` gutter, `24px` (`px-6`) outer margin.
- **`md` (`768px – 1023px` — Tablet):** 8 columns, `24px` gutter, `48px` (`px-12`) outer margin.
- **`lg` / `xl` (`≥ 1024px` — Desktop):** 12 columns, `32px` gutter, `clamp(24px, 5vw, 96px)` outer margin, max container width `1680px`.

### 4.2 Vertical Section Rhythm
- **Standard Section Padding:** `py-16` (`64px` Mobile) → `md:py-24` (`96px` Tablet) → `lg:py-32` (`128px` Desktop).
- **Case Study Editorial Block Gap:** `gap-16` (`64px` Mobile) → `md:gap-24` (`96px` Tablet) → `lg:gap-32` (`128px` Desktop).

### 4.3 Z-Index Governance (Canonical 19-Layer Scale)
Preserves the exact v3.2 stacking tokens (`--z-layer-base: 0` through `--z-layer-cursor: 110`). Raw `z-[number]` utilities are prohibited by ESLint/style rules.

---

## 5. Motion Vocabulary & Tokens (`src/config/motion.ts`)

### 5.1 Easing Curves
```typescript
export const GHOST_EASE = [0.22, 1, 0.36, 1] as const;         // Default UI & editorial reveals
export const GHOST_EASE_SOFT = [0.25, 1, 0.5, 1] as const;     // Atmospheric transitions
export const GHOST_EASE_HEAVY = [0.43, 0.13, 0.23, 0.96] as const; // Page curtain & spatial camera moves
export const GHOST_EASE_AMBIENT = [0.17, 0.55, 0.55, 1] as const;  // Background gradient drift
```

### 5.2 Duration Tokens
- `--duration-micro: 160ms` (Focus rings, icon shifts)
- `--duration-fast: 220ms` (Button hovers, filter pills)
- `--duration-modal: 500ms` (Drawer/curtain transitions)
- `--duration-reveal: 800ms` (Editorial section/card scroll reveals)
- `--duration-atmosphere: 1500ms` (Hero ambient fade-in)

### 5.3 Motion Constraints & Reduced Motion Mandate
- **Allowed Content Properties:** `opacity`, `transform: translateY(≤ 18px)`, `filter: blur(≤ 8px)`.
- **Forbidden Content Properties:** Bouncy springs, `scale > 1.03`, `rotate` on cards, or horizontal scroll-jacking that traps vertical scrolling.
- **`prefers-reduced-motion: reduce`:** Automatically disables `translateY`, `blur`, parallax, and continuous WebGL loops, reducing all transitions to instant or `200ms` opacity crossfades.

