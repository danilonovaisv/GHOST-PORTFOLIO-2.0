# WORKFLOW 12 — VISUAL QA & RESPONSIVE REGRESSION

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/visual-qa` or Phase 12 Visual Verification.
- **Required Context:** `.context/DESIGN-SYSTEM.md`, `.context/CREATIVE-DIRECTION.md`, `.context/QUALITY-GATES.md` (`QG-06`).
- **Participating Agents:** `AG-17` (Visual QA Agent), `AG-03` (Art Director), `AG-07` (UI Engineer).
- **Required Skills:** `visual-regression`, `art-direction`, `portfolio-ux-audit`.
- **Tools:** `run_command` (`pnpm test:e2e`), Playwright MCP, Chrome DevTools MCP.
- **Execution Sequence:**
  1. `PLANNING`: Define the 5-viewport inspection matrix (`375px`, `768px`, `1024px`, `1440px`, `1920px`) across all 9 routes.
  2. `REVIEW`: Check `.std-grid` column alignment, negative space ratio (`≥ 35%`), and z-index stacking order.
  3. `EXECUTION`: Capture full-page Playwright screenshots and execute DOM geometry assertions (`scrollWidth <= clientWidth`).
  4. `VALIDATION`: Verify `QG-06` (`0` horizontal overflows, `0` overlapping z-layers, intact typography scaling).
  5. `CONFIRMATION`: Publish `docs/audits/VISUAL-QA-REPORT.md` with visual evidence.
- **Dependencies:** `06-frontend-development.md`, `09-content-migration.md`.
- **Approval Gates:** Human Art Direction sign-off on captured viewport screenshots.
- **Failure Conditions:** Horizontal overflow on mobile (`375px`), clipped text, or misaligned grid gutters.
- **Recovery Strategy:** Fix responsive Tailwind classes (`min-w-0`, `clamp()`, grid col spans) via `AG-07` and re-capture snapshots.
- **Validation:** `QG-06` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** `docs/audits/VISUAL-QA-REPORT.md` approved across all 5 viewports.

