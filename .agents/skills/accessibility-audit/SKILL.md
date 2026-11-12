---
name: accessibility-audit
version: 2.0.0
origin: Consolidated from a11y-debugging & accessibility-compliance-accessibility-audit in Agent-Skills-Knowledge-Hub
description: Audits and enforces WCAG 2.2 AA compliance across color contrast, keyboard navigation, focus management, ARIA semantics, and reduced motion.
---

# Accessibility Audit Skill (`accessibility-audit`)

## 1. Purpose
Certify that `GHOST-PORTFOLIO-2.0` is 100% accessible to keyboard users, screen readers, and motion-sensitive visitors under **WCAG 2.2 Level AA**.

## 2. When to Use
- During component engineering, Design System token reviews, and Phase 11 (`11-accessibility-audit.md`).

## 3. When Not to Use
- Never certify a route as accessible without running `@axe-core/playwright` and keyboard focus checks.

## 4. Input Contract
- `target_routes`: List of route paths to inspect (`/` through `/contato`).

## 5. Operational Instructions (Progressive Disclosure)
1. **Contrast Audit:** Verify text contrast `≥ 4.5:1` (normal text) and `≥ 3.0:1` (large text & UI boundaries) against `#040013` and `#0B0D3A`.
2. **Keyboard & Focus Audit:** Tab through the entire document; verify skip-to-content link, logical tab order, visible `#4FE6FF` focus ring, and Escape-key dismissal on modals/mobile menu.
3. **Touch & Semantics:** Verify minimum `48x48px` tap targets on mobile, explicit `alt` text on all `<SmartImage />` instances, and `aria-label` on icon-only buttons (`.btn-icon-circle`).
4. **Reduced Motion Audit:** Emulate `prefers-reduced-motion: reduce` and verify all spatial animations and WebGL loops settle cleanly.

## 6. Output Contract
- Accessibility Audit Report (`docs/audits/ACCESSIBILITY-AUDIT.md`) with `QG-07` and `QG-13` status (`PASS` / `FAIL` / `NOT VERIFIED`).

## 7. Validation Criteria
- `0` critical or serious `@axe-core/playwright` violations and Lighthouse Accessibility score `≥ 95`.

