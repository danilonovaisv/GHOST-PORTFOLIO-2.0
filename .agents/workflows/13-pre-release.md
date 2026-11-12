# WORKFLOW 13 — PRE-RELEASE QUALITY GATES & DOSSIER

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/pre-release` or Phase 13 Release Readiness Check.
- **Required Context:** `.context/QUALITY-GATES.md` (`QG-01` through `QG-15`), `.context/SECURITY-ARCHITECTURE.md`.
- **Participating Agents:** `AG-18` (Release Manager), `AG-12` (SEO Engineer), `AG-15` (Security Auditor), `AG-16` (QA Engineer), `AG-00` (Orchestrator).
- **Required Skills:** `deployment-validation`, `security-review`, `seo-optimization`.
- **Tools:** `read_file`, `write_file`, `run_command` (`pnpm typecheck`, `pnpm lint`, `pnpm test`, `pnpm build`, `pnpm test:e2e`).
- **Execution Sequence:**
  1. `PLANNING`: Inventory all 15 Quality Gates (`QG-01`–`QG-15`) and audit reports in `docs/audits/`.
  2. `REVIEW`: Verify security scan (`QG-14`) and technical SEO (`QG-08`: sitemap, robots, JSON-LD, 308 redirects).
  3. `EXECUTION`: Run full clean-build and end-to-end verification pipeline; compile `docs/release/RELEASE-DOSSIER.md`.
  4. `VALIDATION`: Confirm every gate has explicit `PASS` status backed by command output.
  5. `CONFIRMATION`: Transition `.context/active-state.md` to `HUMAN_CONFIRMATION` and present the Release Dossier to Danilo Novais.
- **Dependencies:** `10-performance-audit.md`, `11-accessibility-audit.md`, `12-visual-qa.md`.
- **Approval Gates:** **Mandatory Human Pre-Release Gate** — No staging or production promotion may occur until the Release Dossier is approved.
- **Failure Conditions:** Any gate (`QG-01`–`QG-15`) reporting `FAIL` or lacking execution evidence.
- **Recovery Strategy:** Transition state to `FIX_REQUIRED`, route defect to owning agent, and re-run full pipeline.
- **Validation:** `QG-01` through `QG-15` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** `docs/release/RELEASE-DOSSIER.md` completed with 15/15 gates verified.

