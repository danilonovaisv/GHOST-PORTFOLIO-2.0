# WORKFLOW 04 — GHOST DESIGN SYSTEM 2.0

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/design-system` or Phase 03/05 Design System initialization.
- **Required Context:** `.context/CREATIVE-DIRECTION.md`, `.context/DESIGN-SYSTEM.md`.
- **Participating Agents:** `AG-04` (Design System Architect), `AG-03` (Art Director), `AG-08` (Motion Engineer), `AG-13` (Accessibility Auditor).
- **Required Skills:** `ghost-design-system`, `component-engineering`, `motion-engineering`, `accessibility-audit`.
- **Tools:** `read_file`, `write_file`, `edit_file`, Context7 MCP (`/tailwindlabs/tailwindcss.com`).
- **Execution Sequence:**
  1. `PLANNING`: Audit legacy v3.2 tokens and define Ghost 2.0 `@theme` CSS variables, fluid `clamp()` typography (`Manrope` + `PPSupplyMono`), `.std-grid`, and 19 z-index layers.
  2. `REVIEW`: Verify WCAG 2.2 AA contrast ratios (`≥ 4.5:1`) with `AG-13` and motion curves (`GHOST_EASE`) with `AG-08`.
  3. `EXECUTION`: Codify `src/styles/globals.css`, `src/config/motion.ts`, and atomic primitives in `src/components/ui/` and `src/components/typography/`.
  4. `VALIDATION`: Run `QG-01` (TypeScript), `QG-02` (ESLint), and `QG-07` (Contrast & focus-visible verification).
  5. `CONFIRMATION`: Present token specimen and primitive catalog for human confirmation.
- **Dependencies:** `02-creative-strategy.md`, `03-ux-architecture.md`.
- **Approval Gates:** Human approval of `.context/DESIGN-SYSTEM.md` before building feature pages.
- **Failure Conditions:** Contrast `< 4.5:1`, raw `z-[nnn]` classes, or unapproved font families.
- **Recovery Strategy:** Replace hardcoded values with semantic `@theme` tokens and adjust secondary text lightness (`#B4B8C5`).
- **Validation:** `QG-01`, `QG-02`, `QG-07` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** Design System tokens and atomic UI primitives verified.

