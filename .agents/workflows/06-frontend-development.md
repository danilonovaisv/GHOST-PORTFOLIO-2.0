# WORKFLOW 06 — FRONTEND DEVELOPMENT (ROUTES & COMPONENTS)

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/frontend-dev` or Phases 06–10 Route Implementation.
- **Required Context:** `.context/TECHNICAL-ARCHITECTURE.md`, `.context/COMPONENT-ARCHITECTURE.md`, `.context/DESIGN-SYSTEM.md`.
- **Participating Agents:** `AG-06` (Frontend Architect), `AG-07` (UI Engineer), `AG-11` (Media Pipeline Engineer), `AG-16` (QA Engineer).
- **Required Skills:** `nextjs-architecture`, `component-engineering`, `ghost-design-system`, `media-optimization`.
- **Tools:** `read_file`, `write_file`, `edit_file`, `run_command`, Context7 MCP.
- **Execution Sequence:**
  1. `PLANNING`: Define Server vs. Client Component tree for the target route(s) (`/`, `/portfolio`, `/projetos/[slug]`, `/sobre`, `/expertise`, `/creative-technology`, `/lab`, `/curriculo`, `/contato`).
  2. `REVIEW`: Verify RSC boundaries, `error.tsx` segment boundaries, and `generateStaticParams` contracts with `AG-06`.
  3. `EXECUTION`: Implement route pages, `<CaseBlockRenderer />` blocks, and `<SmartImage />` / `<AdaptiveVideo />` integration.
  4. `VALIDATION`: Execute `QG-01` (`pnpm typecheck`), `QG-02` (`pnpm lint`), `QG-04` (Integration tests), and `QG-06` (Responsive check).
  5. `CONFIRMATION`: Present completed route(s) with verification logs.
- **Dependencies:** `05-prototyping.md`.
- **Approval Gates:** Human review after each major route milestone (Home → Portfolio & Cases → Institutional & Tech).
- **Failure Conditions:** Unnecessary `'use client'` at route root, TypeScript errors, or horizontal mobile overflow.
- **Recovery Strategy:** Extract interactive state into leaf Client Islands and enforce `.std-grid` constraints.
- **Validation:** `QG-01`, `QG-02`, `QG-04`, `QG-06`, `QG-10`, `QG-11` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** Target routes render cleanly across all viewports with zero type/lint errors.

