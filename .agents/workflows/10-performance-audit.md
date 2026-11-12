# WORKFLOW 10 — PERFORMANCE & CORE WEB VITALS AUDIT

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/performance-audit` or Phase 10/11 Performance Verification.
- **Required Context:** `.context/QUALITY-GATES.md`, `.context/MEDIA-ARCHITECTURE.md`, `.context/TECHNICAL-ARCHITECTURE.md`.
- **Participating Agents:** `AG-14` (Performance Auditor), `AG-06` (Frontend Architect), `AG-09` (Creative Tech Engineer), `AG-11` (Media Pipeline Engineer).
- **Required Skills:** `performance-audit`, `media-optimization`, `threejs-experience`.
- **Tools:** `run_command`, Chrome DevTools MCP (`lighthouse_audit`, `performance_start_trace`, `performance_stop_trace`).
- **Execution Sequence:**
  1. `PLANNING`: Build production artifact (`pnpm build`) and start local production server (`pnpm start`).
  2. `REVIEW`: Identify routes with highest media/WebGL density (`/`, `/portfolio`, `/projetos/[slug]`, `/creative-technology`, `/lab`).
  3. `EXECUTION`: Run Lighthouse Mobile & Desktop audits, bundle size analysis, and main-thread/GPU frame traces.
  4. `VALIDATION`: Verify `QG-09` (Lighthouse Performance `≥ 90`, `LCP < 2.5s`, `INP < 200ms`, `CLS < 0.1`), `QG-10` (Images), `QG-11` (Videos), and `QG-12` (WebGL 60fps).
  5. `CONFIRMATION`: Write `docs/audits/PERFORMANCE-AUDIT.md` with execution evidence.
- **Dependencies:** `06-frontend-development.md`, `08-motion-development.md`, `09-content-migration.md`.
- **Approval Gates:** Blocks release if mobile or desktop Lighthouse Performance `< 90`.
- **Failure Conditions:** `LCP > 2.5s`, `CLS > 0.1`, `INP > 200ms`, or First Load JS `> 180KB` on editorial routes.
- **Recovery Strategy:** Lazy-load below-the-fold client islands, compress LCP poster/image, and reduce initial JS payload.
- **Validation:** `QG-09`, `QG-10`, `QG-11`, `QG-12` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** `docs/audits/PERFORMANCE-AUDIT.md` certifies `PASS` on all CWV gates.

