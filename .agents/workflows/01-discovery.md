# WORKFLOW 01 — DISCOVERY & ECOSYSTEM AUDIT

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/discovery` or Phase 00 initialization.
- **Required Context:** `.context/PROJECT-CONSTITUTION.md`, `PORTFOLIO-DANILO-FINAL` (read-only), `Agent-Skills-Knowledge-Hub` (read-only).
- **Participating Agents:** `AG-00` (Orchestrator), `AG-01` (Creative Strategist), `AG-02` (UX Architect), `AG-06` (Frontend Architect).
- **Required Skills:** `portfolio-context`, `portfolio-ux-audit`.
- **Tools:** `read_file`, `write_file`, GitHub MCP (`get_file_contents`), `search_web`.
- **Execution Sequence:**
  1. `PLANNING`: Define audit scope across live site (`portfoliodanilo.com`), legacy repository (`PORTFOLIO-DANILO-FINAL`), and `Agent-Skills-Knowledge-Hub`.
  2. `REVIEW`: Verify read-only access boundaries (`Law #1`).
  3. `EXECUTION`: Inspect routes, `package.json`, `globals.css`, `supabase/schema.sql`, `.agents/`, and Knowledge Hub catalog; compile `docs/research/DISCOVERY_REPORT.md`.
  4. `VALIDATION`: Verify every architectural claim separates **Verified Facts** from **Assumptions**.
  5. `CONFIRMATION`: Present `DISCOVERY_REPORT.md` to human principal.
- **Dependencies:** `00-project-onboarding.md`.
- **Approval Gates:** Human sign-off on Discovery findings at Phase 09 gate.
- **Failure Conditions:** Any attempt to mutate `PORTFOLIO-DANILO-FINAL` or rely on unverified assumptions.
- **Recovery Strategy:** Revert any non-local change immediately; re-verify facts via GitHub MCP.
- **Validation:** `DISCOVERY_REPORT.md` completeness check (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** `docs/research/DISCOVERY_REPORT.md` written and traceable to source files.

