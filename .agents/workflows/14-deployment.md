# WORKFLOW 14 — STAGED DEPLOYMENT & PRODUCTION CUTOVER

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/deploy` or Phase 14 Deployment (Strictly after `13-pre-release.md` approval).
- **Required Context:** `docs/release/RELEASE-DOSSIER.md`, `.context/SECURITY-ARCHITECTURE.md`, `.context/TECHNICAL-ARCHITECTURE.md`.
- **Participating Agents:** `AG-18` (Release Manager), `AG-00` (Project Orchestrator), `AG-16` (QA Engineer).
- **Required Skills:** `deployment-validation`, `security-review`.
- **Tools:** `read_file`, `run_command`, GitHub MCP.
- **Execution Sequence:**
  1. `PLANNING`: Verify target environment (`staging` preview URL first; never overwrite live `portfoliodanilo.com` directly).
  2. `REVIEW`: Confirm explicit human authorization for deployment (`Law #1`, `Law #8`).
  3. `EXECUTION`: Deploy to isolated Staging URL; execute live smoke tests (`QG-05`, `QG-08`, `QG-14` HTTP headers) against Staging.
  4. `VALIDATION`: Verify `200 OK` on all 9 routes, `308` redirects on legacy paths, CSP headers, and asset loading on Staging.
  5. `CONFIRMATION`: Present live Staging URL to Danilo Novais and wait for explicit final authorization before any DNS cutover of `portfoliodanilo.com`.
- **Dependencies:** `13-pre-release.md`.
- **Approval Gates:**
  - **Gate 14-A:** Explicit human approval before deploying to Staging.
  - **Gate 14-B:** Explicit human approval after Staging inspection before switching `portfoliodanilo.com` production domain.
- **Failure Conditions:** Any post-deploy smoke test failure, CSP block, or unauthorized production mutation.
- **Recovery Strategy:** Instant rollback to previous deployment / keep `portfoliodanilo.com` pointed at untouched original production host.
- **Validation:** Live Staging Smoke Suite (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** Staging verified, human confirmation recorded, and deployment logged in `.context/DECISION-LOG.md`.

