# WORKFLOW 00 — PROJECT ONBOARDING & CONTEXT CALIBRATION

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/onboard` or initial session startup in any IDE (Google Antigravity, Claude Code, Cursor, Codex).
- **Required Context:** `.context/PROJECT-CONSTITUTION.md`, `.context/active-state.md`, `.context/DECISION-LOG.md`, `.agents/AGENTS_MANIFEST.md`.
- **Participating Agents:** `AG-00` (Project Orchestrator).
- **Required Skills:** `portfolio-context`.
- **Tools:** `read_file` (scoped to `.context/` and `.agents/`).
- **Execution Sequence:**
  1. `PLANNING`: Read `.context/active-state.md` and `.context/PROJECT-CONSTITUTION.md`.
  2. `REVIEW`: Identify current workflow phase and any active human approval gates.
  3. `EXECUTION`: Load only the specialist agent and skill definitions required for the current phase.
  4. `VALIDATION`: Confirm workspace cleanliness (`git status`) and environment readiness.
  5. `CONFIRMATION`: Report current PREVC state and await task instruction.
- **Dependencies:** None (Root entry workflow).
- **Approval Gates:** Pause if `.context/active-state.md` is in `REVIEW_REQUIRED` or `HUMAN_CONFIRMATION`.
- **Failure Conditions:** Missing `.context/PROJECT-CONSTITUTION.md` or corrupted workspace state.
- **Recovery Strategy:** Restore `.context/` files from git HEAD and halt execution until verified.
- **Validation:** Verify `.context/active-state.md` is readable (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** Agent session calibrated with zero unauthorized file mutations.

