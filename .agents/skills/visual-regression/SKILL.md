---
name: visual-regression
version: 2.0.0
origin: Adapted from audit-validator & verify-portfolio-change in PORTFOLIO-DANILO-FINAL and Agent-Skills-Knowledge-Hub
description: Performs multi-viewport visual regression comparisons (375px to 1920px), verifying .std-grid alignment, z-index stacking, and zero horizontal overflow.
---

# Visual Regression & Responsive QA Skill (`visual-regression`)

## 1. Purpose
Verify visual fidelity, responsive layout integrity, and `.std-grid` alignment across mobile, tablet, and desktop viewports (`375px`, `768px`, `1024px`, `1440px`, `1920px`).

## 2. When to Use
- After any UI, typography, or motion change, and during Phase 12 (`12-visual-qa.md`).

## 3. When Not to Use
- Never skip mobile (`375px`) or tablet (`768px`) checks when validating desktop changes.

## 4. Input Contract
- `routes`: Target routes to snapshot and inspect.
- `viewports`: `[375, 768, 1024, 1440, 1920]`.

## 5. Operational Instructions (Progressive Disclosure)
1. **Multi-Viewport Capture:** Use Playwright (`tests/visual/`) to render each route across all 5 widths.
2. **Overflow & Geometry Check:** Assert `document.documentElement.scrollWidth <= document.documentElement.clientWidth` on every viewport.
3. **Z-Layer & Stacking Check:** Verify that header (`55`), mobile header (`80`), mobile curtain (`90`), and modals (`100`) never collide with foreground text (`20`) or 3D canvases (`15–30`).
4. **Ghost Token Check:** Confirm computed background (`#040013`), primary accent (`#0048FF`), and `Manrope` / `PPSupplyMono` font loading.

## 6. Output Contract
- Visual QA Matrix Report (`docs/audits/VISUAL-QA-REPORT.md`) with screenshot artifacts and `QG-06` status.

## 7. Validation Criteria
- `QG-06` reports `PASS` across all 5 viewports with zero layout breaks or horizontal scrollbars.

