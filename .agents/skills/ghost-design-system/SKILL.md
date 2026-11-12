---
name: ghost-design-system
version: 2.0.0
origin: Evolved from ghost-design (v3.2) & criar-design-system in PORTFOLIO-DANILO-FINAL and Agent-Skills-Knowledge-Hub
description: Enforces Ghost Design System 2.0 tokens (@theme colors, Manrope + PPSupplyMono clamp typography, .std-grid, 19 z-index layers, and CTA primitives).
---

# Ghost Design System 2.0 Skill (`ghost-design-system`)

## 1. Purpose
Guarantee 100% token consistency across CSS and React components using **Ghost Design System 2.0**.

## 2. When to Use
- Whenever writing or reviewing Tailwind CSS v4 classes, CSS variables in `src/styles/globals.css`, or UI components in `src/components/`.

## 3. When Not to Use
- Never invent ad-hoc hex colors, inline `cubic-bezier` curves, or arbitrary `z-[nnn]` values outside the canonical token table.

## 4. Input Contract
- `component_or_stylesheet`: Target `.tsx` or `.css` file.

## 5. Operational Instructions (Progressive Disclosure)
1. **Color Governance:** Use canonical tokens (`--color-background: #040013`, `--color-bluePrimary: #0048FF`, `--color-blueAccent: #4FE6FF`, `--color-neutral: #0B0D3A`, `--color-text: #FCFFFF`, `--color-text-secondary: #B4B8C5`). Restrict `#8705F2` (Purple) strictly to hover/anomaly states.
2. **Typography Governance:** Use `Manrope` Variable (`--font-sans`) for display/UI/body with fluid `clamp()` utilities (`.text-hero-manifesto`, `.text-display`, `.text-h1`–`.text-h3`, `.text-body-editorial`) and `PPSupplyMono` (`--font-mono`) for technical metadata (`.text-micro-mono`).
3. **Grid & Z-Index Governance:** Wrap major sections in `<StandardGrid />` (`.std-grid`, `4 / 8 / 12` cols, `max-w-[1680px]`) and use semantic `--z-layer-*` variables (`0`–`110`).
4. **Deep Reference:** Load `.context/DESIGN-SYSTEM.md` for full token tables and contrast ratios.

## 6. Output Contract
- Token-compliant CSS/JSX code with zero magic numbers or unapproved color/z-index literals.

## 7. Validation Criteria
- `QG-02` (`pnpm lint`) and `QG-07` (WCAG 2.2 AA contrast `≥ 4.5:1`) pass with zero token violations.

