---
name: portfolio-ux-audit
version: 2.0.0
origin: Reused & adapted from Portfolio Design Auditor (design-auditor & auditoria-estrategica-portfolio) in Agent-Skills-Knowledge-Hub
description: Executes evidence-based UX, usability, hierarchy, conversion journey, and mobile ergonomics audits with P0–P3 findings.
---

# Portfolio UX Audit Skill (`portfolio-ux-audit`)

## 1. Purpose
Evaluate user experience, visual hierarchy, executive conversion flows, and mobile ergonomics across `GHOST-PORTFOLIO-2.0`, producing prioritized (`P0`–`P3`) actionable findings.

## 2. When to Use
- During Phase 00 (Discovery), Phase 02/04 (Wireframe & Prototype review), and Phase 11/12 (Accessibility & Visual QA).

## 3. When Not to Use
- Do not treat subjective aesthetic opinion as a UX defect; every finding must cite code, DOM geometry, or WCAG/usability heuristics.

## 4. Input Contract
- `target_route`: Route URL or component path.
- `viewport_matrix`: `375px` (Mobile), `768px` (Tablet), `1440px` (Desktop).

## 5. Operational Instructions (Progressive Disclosure)
1. **Executive 10-Second Test:** Verify above-the-fold clarity of Danilo's positioning and primary CTA (`<AntigravityCTA />`).
2. **2-Click Conversion Check:** Verify that Portfolio cases, Executive CV (`/curriculo`), and Contact (`/contato`) are reachable within 2 interactions.
3. **Mobile & Touch Ergonomics:** Verify touch targets `≥ 48x48px`, safe-area padding, and zero scroll/drag gesture conflicts.
4. **Deep Reference:** Load `.context/INFORMATION-ARCHITECTURE.md` and `.context/DESIGN-SYSTEM.md` for structural baselines.

## 6. Output Contract
Structured findings using the canonical `Portfolio Design Auditor` format:
- `AUD-[NUM]` — Title, Target, Category, Priority (`P0`–`P3`), Observation, Evidence, Recommendation, Preserve Clause, and Acceptance Criteria.

## 7. Validation Criteria
- Every finding includes concrete DOM/code evidence and measurable acceptance criteria.

