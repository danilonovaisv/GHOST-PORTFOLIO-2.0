# WORKFLOW 07 — BACKEND, DATA REPOSITORY & VALIDATION LAYER

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/backend-dev` or Phase 05/07 Data Layer Implementation.
- **Required Context:** `.context/DATABASE-SCHEMA.md`, `.context/SECURITY-ARCHITECTURE.md`, `.context/TECHNICAL-ARCHITECTURE.md`.
- **Participating Agents:** `AG-10` (Backend Engineer), `AG-06` (Frontend Architect), `AG-15` (Security Auditor), `AG-16` (QA Engineer).
- **Required Skills:** `nextjs-architecture`, `security-review`.
- **Tools:** `read_file`, `write_file`, `edit_file`, `run_command`, Context7 MCP (`/supabase/ssr/v0.12.7`).
- **Execution Sequence:**
  1. `PLANNING`: Define Zod 4 schemas (`src/lib/validation/`), data repository functions (`src/lib/data/`), and tagged cache rules (`unstable_cache`).
  2. `REVIEW`: Audit security boundaries (`import 'server-only'`) and read-only production safety (`Law #1`) with `AG-15`.
  3. `EXECUTION`: Implement `src/lib/validation/content-schema.ts`, `src/lib/data/projects.ts`, `src/lib/data/experiences.ts`, snapshot fallback loader, and `/contato` Server Action.
  4. `VALIDATION`: Run `QG-01` (TypeScript), `QG-03` (Unit & Zod validation tests), and `QG-14` (Security boundary check).
  5. `CONFIRMATION`: Record verified repository status in `.context/active-state.md`.
- **Dependencies:** `02-creative-strategy.md`.
- **Approval Gates:** Explicit human approval required before creating any `ghost_v2` tables in remote Supabase.
- **Failure Conditions:** Mutation of `public.*` production tables, missing Zod validation, or leaked server keys.
- **Recovery Strategy:** Immediately halt DB operations, enforce local snapshot mode, and rotate any exposed key.
- **Validation:** `QG-01`, `QG-03`, `QG-14` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** Data repositories return 100% Zod-validated entities with automatic snapshot resilience.

