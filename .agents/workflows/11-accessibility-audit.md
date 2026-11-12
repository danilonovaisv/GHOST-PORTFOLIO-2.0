# WORKFLOW 11 — ACCESSIBILITY AUDIT (WCAG 2.2 AA)

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/accessibility-audit` or Phase 11 Accessibility Verification.
- **Required Context:** `.context/DESIGN-SYSTEM.md`, `.context/QUALITY-GATES.md` (`QG-07`, `QG-13`).
- **Participating Agents:** `AG-13` (Accessibility Auditor), `AG-07` (UI Engineer), `AG-08` (Motion Engineer).
- **Required Skills:** `accessibility-audit`, `ghost-design-system`.
- **Tools:** `run_command`, Playwright MCP (`@axe-core/playwright`), Chrome DevTools MCP.
- **Execution Sequence:**
  1. `PLANNING`: Configure Axe-core + Playwright scan across all 9 routes in standard and reduced-motion modes.
  2. `REVIEW`: Inspect semantic heading hierarchy (`h1`–`h3`), landmark roles (`main`, `nav`, `footer`), and form labels on `/contato`.
  3. `EXECUTION`: Run automated Axe scans, manual keyboard-only Tab traversal, focus-trap tests on `<MobileMenuCurtain />`, and `prefers-reduced-motion: reduce` checks.
  4. `VALIDATION`: Verify `QG-07` (`0` critical/serious Axe issues, contrast `≥ 4.5:1`, touch targets `≥ 48x48px`) and `QG-13` (Reduced motion).
  5. `CONFIRMATION`: Write `docs/audits/ACCESSIBILITY-AUDIT.md` with full execution logs.
- **Dependencies:** `06-frontend-development.md`, `08-motion-development.md`.
- **Approval Gates:** Blocks release if any critical/serious WCAG 2.2 AA violation is detected.
- **Failure Conditions:** Missing `alt` attributes, invisible focus rings, keyboard traps, or contrast `< 4.5:1`.
- **Recovery Strategy:** Remediate component semantics/tokens via `AG-07`/`AG-08` and re-run Axe verification.
- **Validation:** `QG-07` & `QG-13` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** `docs/audits/ACCESSIBILITY-AUDIT.md` certifies `PASS` across all 9 routes.

